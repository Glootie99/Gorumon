# El servidor de Factucoin: qué montar, cómo crecer y qué hay que cumplir

> Investigación del 05-11-2026 para la tarea de Adrián. Casi todos los precios salen de agregadores, porque en la investigación no se pudieron abrir las webs oficiales; al final hay una lista de lo que hay que verificar. Nada de esto es asesoría legal.

## 1. La recomendación

**Montamos el programa en contenedores sobre un VPS Hetzner CX33 en Alemania (Linux, sin Mac), por unos 10-13 €/mes más céntimos de IA, con HTTPS, una clave de cifrado por gestoría, doble factor, el servidor cerrado salvo el puerto 443, copias cifradas e imborrables en otro proveedor de la UE, un pentest antes del primer cliente real y un contrato de encargo con cada gestoría.**

Por qué esta opción y no otra:
- **Barato al empezar, sin rehacer nada al crecer.** Cada gestoría ya tiene su propio fichero de base de datos (SQLite). Para crecer se añaden servidores y se reparten gestorías, en vez de mudarse a otra plataforma.
- **Las nubes grandes no compensan todavía.** AWS, Azure o Google cuestan de 4 a 8 veces más hasta las 30 gestorías. Solo merecen la pena si un cliente exige la certificación española ENS Alto o si conseguís créditos para startups.
- **Un ordenador en casa no sirve de servidor principal.** Los contratos de fibra doméstica pueden prohibirlo, una gestoría no puede auditar una casa, y si se va la luz el día 19 no hay servicio.
- **La IA no es un problema de dinero, sino de dónde se procesan los datos.** Cuesta entre céntimos y unos 90 $/mes incluso con 30 gestorías.

## 2. Lo esencial del servidor

### Las opciones comparadas

Cifras mensuales sin IVA. Las sumas son **cálculo propio** con los precios citados; «≈» significa estimación, no presupuesto.

| Opción | 1 gestoría | 3 | 10 | 30 | Confianza ante una gestoría | Pega principal |
|---|---|---|---|---|---|---|
| **VPS europeo (Hetzner/OVH)** ✅ | ≈10-12 € | ≈13-16 € | ≈25-40 € | ≈50-90 € | Media-alta | Mantenimiento propio |
| Nube grande en región UE/España | ≈45 $ | ≈45-90 $ | ≈100-150 $ | ≈200-350 $ | Alta (ENS Alto) | Cara y con costes ocultos |
| PaaS / contenedores gestionados UE | ≥36 € | ≥36 € | Sube con el uso | Sube con el uso | Media-alta | La web siempre encendida sale cara |
| Todo en un Mac en casa | ≈35-50 € | ≈35-50 € | No escala | No viable | Baja | Contrato doméstico, cortes, no auditable |
| Mac alquilado en la UE | 149 € | 149 € | 149-199 € | ≈300-400 € | Alta | Caro para empezar |

**Precios de referencia:**
- **Hetzner**, tras las dos subidas de 2026 (abril, +30-37 %, y 15 de junio): CX23 (2 vCPU/4 GB) a **5,49 €**, CX33 (4 vCPU/8 GB) a **8,49-8,99 €** y CX43 (8 vCPU/16 GB) a **15,99 €**, más **0,50 €** de IPv4 ([bitdoze](https://www.bitdoze.com/hetzner-cloud-review/); [stackvaluelab](https://stackvaluelab.com/hetzner-price-increase-2026/); [bitdoze ES](https://www.bitdoze.com/es/hetzner-cloud-precios-2026/)). La subida de junio también se aplica al **cambiar de tamaño** un servidor existente ([rscomputers-ks](https://rscomputers-ks.com/hetzner-price-increase-2026-move-servers/)), así que conviene crecer añadiendo servidores. Hubo informes de **falta de stock** de los planes CX ([stackvaluelab](https://stackvaluelab.com/hetzner-cx-cax-unavailable/)).
- **Alternativa: OVHcloud.** VPS-1 a unos **6,49 €** y VPS-2 a **9,99 €** ([vpsledger](https://vpsledger.com/providers/ovhcloud/)), y figura con ENS Alto en un listado de terceros ([cloudlandscape](https://cloudlandscape.github.io/en/providers/ovhcloud/)).
- **Nube grande:** el mínimo en AWS ronda los **45 $/mes** (máquina t4g.medium, base de datos RDS micro e IPv4) ([aws-pricing.com](https://aws-pricing.com/t4g.medium.html); [bytebase](https://www.bytebase.com/dbcost/rds/instance/db.t4g.micro/)). AWS tiene ENS Alto en 166 servicios ([AWS](https://aws.amazon.com/blogs/security/aws-achieves-spains-ens-high-certification-across-166-services)).
- **Copias:** Scaleway Object Storage, unos **0,0146 €/GB al mes** ([Scaleway](https://www.scaleway.com/fr/tarifs/storage)), es decir, ≈1,5 € por 100 GB. Una segunda copia en Hetzner Storage Box (1 TB) cuesta **3,20 €** ([whtop](https://www.whtop.com/amp/plans/hetzner.com/128269)).

### Cómo se crece sin rehacer nada

Tres reglas desde el primer día: **todo en contenedores Docker**, el **OCR pesado como trabajadores que cogen tareas de una cola** y **un fichero de base de datos por gestoría**.

| Escalón | Qué hay | Coste al mes (sin IVA ni IA) | Cuándo subir |
|---|---|---|---|
| **0-1 gestorías** | 1 Hetzner CX33 + IPv4 con la web, la cola, las bases y el OCR; copia cifrada en Scaleway | **≈10-12 €** | Cuando el cierre sature la CPU o firme la 2.ª-3.ª gestoría |
| **3** | Igual, más una segunda copia en Storage Box | **≈13-16 €** | Cuando la cola de un día 20 tarde horas |
| **10** | Servidor CX43 para la aplicación + trabajadores de OCR que se encienden por horas en la semana de cierre | **≈25-40 €** | Cuando un servidor no aguante el pico |
| **30** | 2-3 servidores CX43 con las gestorías repartidas + trabajadores en el pico | **≈50-90 €** | Valorar PostgreSQL gestionado solo si hace falta consultar varias gestorías a la vez |

El coste está en los **picos de la semana del día 20** de enero, abril, julio y octubre, no en el día a día. Por eso conviene un servidor pequeño que sume trabajadores por horas. Que Hetzner cobre por horas está por verificar.

### La IA en el servidor

Supuestos: cada factura que llega a la IA consume **3.000 tokens de entrada y 500 de salida**. A modo ilustrativo, 1 gestoría ≈ 1.000 facturas al mes, 10 ≈ 10.000 y 30 ≈ 50.000, y el 30 % llega a la IA. Alex debe sustituir estas cifras por las reales.

| Modelo y vía | $/factura | 1 gestoría | 10 | 30 | ¿Procesa en la UE? |
|---|---|---|---|---|---|
| Claude Haiku 5.5, API directa | 0,00055 | 0,16 $ | 1,65 $ | 8,25 $ | **No** (solo «global» o «us») |
| Claude Haiku 4.5 en AWS Bedrock UE | 0,00605 | 1,81 $ | 18,15 $ | 90,75 $ | Sí, incluye España |
| Mistral Small 4 | 0,00075 | 0,22 $ | 2,25 $ | 11,25 $ | Sí, por defecto |
| GPT-5.4 nano, proyecto Europa | 0,00122 | 0,37 $ | 3,67 $ | 18,38 $ | Sí |

Fuentes: [precios Claude](https://platform.claude.com/docs/en/about-claude/pricing); [residencia de datos de Anthropic](https://platform.claude.com/docs/en/manage-claude/data-residency); [Bedrock UE](https://docs.aws.eu/bedrock/latest/userguide/model-card-anthropic-claude-opus-4-6.html); [Mistral](https://pricepertoken.com/pricing-page/model/mistral-ai-mistral-small); [GPT nano](https://costbench.com/software/llm-api-providers/openai-api/).

**Recomendación:** empezar con **Claude en Bedrock con perfil UE**, o con Mistral como alternativa, porque los datos se quedan en la UE. Con Haiku 4.5 es más caro que la API directa, pero la diferencia en el peor caso son unos 80 $/mes con 30 gestorías. **Si se confirma Haiku 5.5 en Bedrock UE**, el coste con 30 gestorías bajaría a unos **9 $/mes** (verificación del 05-11-2026). Está pendiente de confirmar el precio en la página oficial de Bedrock, si el perfil UE lleva el +10 % y si la cuenta tiene acceso al modelo. Mistral aloja en la UE por defecto, pero algunas funciones se procesan fuera: hay que revisar su lista de subencargados. Un modelo propio en una GPU no compensa: la más barata cuesta unos **184 €/mes** ([Hetzner](https://www.hetzner.com/gpu)).

### Seguridad mínima

| Medida | Cómo | Coste |
|---|---|---|
| HTTPS | Caddy con certificados automáticos | 0 € |
| Cifrado | Disco cifrado y una clave por gestoría (sops + age); al dar de baja una gestoría, se borra su clave | 0 € |
| Acceso | Doble factor y roles por gestoría; administración interna solo por WireGuard | 0 € |
| Aislamiento | Una base por gestoría y pruebas automáticas de acceso cruzado | 0 € |
| Exposición mínima | Cortafuegos con todo cerrado salvo el puerto 443 | 0 € |
| Subidas de ficheros | Comprobar el tipo real del fichero, antivirus ClamAV y OCR en un contenedor sin red | 0 € |
| Mantenimiento | Parches automáticos, Trivy y Dependabot | 0 € |
| Avisos | Uptime Kuma o el plan gratuito de Better Stack | 0 € |
| Copias | restic cifrado a otro proveedor de la UE, con bloqueo de borrado (Object Lock) y una restauración de prueba cada trimestre | ≈1,5-5 €/mes |
| Registro de accesos | Registro que no se pueda borrar, guardado fuera del servidor | 0 a pocos €/mes |

Fuentes: [OWASP subidas](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html); [restic](https://restic.readthedocs.io/); [OVH Object Lock](https://docs.ovhcloud.com/en/guides/storage-and-backup/object-storage/s3-faq).

Cloudflare Pro (WAF, 20-25 $/mes) es opcional y tiene un coste de privacidad: Cloudflare vería las facturas sin cifrar y pasaría a ser un subencargado más ([selfhosted-sh](https://selfhosted-sh.pages.dev/cloudflare-tunnels-zero-trust-access)).

## 3. El pentest: punto de control, no un precio más

El pentest es una **puerta**. **Ninguna factura real entra en el servidor hasta que se haya hecho y se hayan arreglado los fallos graves.** Es lo que permite decirle a una gestoría «lo ha revisado un tercero» en vez de «confía en nosotros», y lo que más pesa si algún día hay una brecha.

**Qué debe probar, como mínimo:**
1. **Que una gestoría no pueda ver los datos de otra**, ni por la web, ni por la API, ni adivinando enlaces de ficheros. Es el fallo más grave posible en este negocio.
2. **El inicio de sesión:** doble factor, robo de sesión, fuerza bruta y recuperación de contraseña.
3. **Las subidas de ficheros:** PDFs maliciosos, ficheros que no son lo que dicen y tamaños enormes.
4. **La API:** permisos de cada petición y datos personales en los mensajes de error.
5. **El servidor por fuera:** puertos abiertos, versiones con fallos conocidos y configuración de HTTPS.
6. **Las copias:** que no se puedan leer ni borrar con las credenciales del servidor.

**Cuándo:**
- **Antes:** revisión propia con herramientas gratuitas (OWASP ZAP, Trivy, Semgrep y Gitleaks, que la Factory ya tiene). Aquí tu perfil de ciberseguridad aporta mucho y abarata el pentest, porque se llega con lo fácil ya arreglado.
- **Pentest externo:** con el servidor montado, **antes del primer cliente real**. No antes del servidor de juguete.
- **Repetirlo:** tras cambios grandes, como una API nueva o una nueva forma de subir facturas, y como mínimo una vez al año.
- **Comprobar los arreglos:** que el proveedor vuelva a probar los fallos que encontró (retest).

**Coste orientativo:** desde 1.490 € con un alcance muy acotado; lo habitual en una web sencilla, **2.000-6.000 €** ([Hard2bit](https://hard2bit.com/blog/cuanto-cuesta-un-pentesting-en-espana/)). Desconfiad de los precios muy bajos: suelen ser solo un escaneo automático. Pedid tres presupuestos con el alcance de arriba por escrito.

## 4. Objeción: ¿hace falta un Mac?

El programa de Alex tiene dos lectores de imagen (OCR). **RapidOCR**, el principal, funciona en Linux. **Apple Vision**, el de rescate, solo existe en macOS. Por eso salía un Mac en el montaje. **No es imprescindible**, y empezar sin él es más simple, barato y fácil de explicar a una gestoría.

**Alternativas en Linux para el rescate:**
- **Un segundo OCR gratuito** en el mismo servidor: PaddleOCR, Surya, docTR o Tesseract.
- **La IA con imagen** (Haiku o Mistral) para lo que el OCR no lea bien. Ya está en la cascada y cuesta céntimos.
- **OCR de pago en la nube con región UE**, como Azure Document Intelligence, AWS Textract, Google Document AI o Mistral OCR, por céntimos por página. Añade un subencargado.

**Cómo decidirlo:** Alex puede apagar Apple Vision con `FAC_VISION=0` y medir cuánto empeora la lectura con las mismas facturas. Si la diferencia es pequeña, el Mac sobra. Si es grande, se añade después sin cambiar nada más:
- **Un Mac alquilado en París (Scaleway)** solo en la semana de cierre: 0,22 €/h con un mínimo de 24 h, unos **37 € por trimestre** ([Scaleway](https://scaleway.com/en/pricing/apple-silicon)). O fijo desde **149 €/mes**.
- **El Mac de casa como trabajador**: sale a buscar tareas por WireGuard, procesa en memoria y no guarda nada. Es la opción más barata, pero el domicilio pasa a ser un lugar de tratamiento que hay que declarar a la gestoría, y la línea doméstica puede no permitir uso comercial ([condiciones de ejemplo](https://www.marianoacosta.coop/wp-content/uploads/2019/10/Condiciones-Particulares-y-Generales-WEB.pdf)).

## 5. Lo legal: qué hay que tener antes de tratar facturas reales

**¿Lo hemos revisado todo?** Los puntos de abajo cubren lo que pide el RGPD a un encargado del tratamiento. Pero en la investigación no se pudieron abrir los documentos de la AEPD (su web está bloqueada en la sesión), y varias cosas están marcadas «a confirmar». Antes de abrir el servidor a gestorías que no conocéis, **un profesional de protección de datos debe revisar esta lista**. Para el piloto por Drive basta con la plantilla bien hecha (punto 2).

**1. Quién es quién.** La **gestoría es la responsable** de los datos de sus clientes; **vosotros sois sus encargados** (art. 28 del RGPD). Solo podéis hacer con los datos lo que ella os encargue.

**2. Contrato de encargo con cada gestoría** (art. 28.3). Adaptado a cada caso: la AEPD ha sancionado contratos genéricos ([Fieldfisher](https://www.fieldfisher.com/es-es/locations/spain/insights/mala-gestion-multa)). Debe decir:
- qué datos, para qué, cuánto tiempo y dónde se tratan;
- que solo seguís sus instrucciones y guardáis confidencialidad;
- las medidas de seguridad (la tabla del apartado 2);
- quiénes son los subencargados (punto 3);
- que les ayudáis con los derechos de sus clientes y con las brechas;
- qué pasa al terminar: **devolver o borrar** todos los datos, también los de las copias;
- que pueden auditaros.

Hay directrices oficiales para redactarlo ([AEPD](https://aepd.es/guias/guia-directrices-contratos.pdf)) y la herramienta gratuita **Facilita RGPD / Facilita EMPRENDE** genera borradores ([AEPD](https://www.aepd.es/guias-y-herramientas/herramientas/facilita-emprende)). Ojo: Facilita es solo para tratamientos de **riesgo bajo** y excluye los tratamientos masivos. Sirve para el piloto; con muchas gestorías, el contrato debe revisarlo un profesional. Que la AEPD haya sancionado contratos genéricos lo dice un despacho de abogados, no la AEPD: está sin confirmar.

**3. Subencargados, con autorización por escrito.** Todos los que tocan datos: el servidor (Hetzner), las copias (Scaleway), la IA (AWS o Mistral) y Cloudflare si se usa. **Para el piloto, Google Drive también lo es.** La guía de la AEPD pide **autorización previa por escrito**, que puede ser específica (proveedor a proveedor) o general. Si es general, hay que **avisar de cada cambio y dar un plazo para oponerse**. Hay que listarlos con nombre, domicilio y qué hacen ([IAPP sobre el CEPD](https://iapp.org/news/a/controllers-processors-and-subprocessors-in-chains)). Si algún día se usa el Mac de casa, ese domicilio también se declara.

**4. Transferencias fuera de la UE.** Si la IA procesa en EE. UU. (la API directa de Anthropic, por ejemplo), es una transferencia internacional. Se ampara en el marco UE-EE. UU. (DPF) y en cláusulas tipo, pero el DPF tiene un recurso pendiente ante el Tribunal de Justicia de la UE ([WilmerHale](https://www.wilmerhale.com/insights/blogs/wilmerhale-privacy-and-cybersecurity-law/20251201-european-court-of-justice-to-review-challenge-to-eu-us-data-privacy-framework)). **Por eso se recomienda IA con procesamiento en la UE**, y pedir siempre que no se guarden los datos (retención cero) y que no se usen para entrenar.

**5. Registro de actividades como encargados** (art. 30.2). Un documento corto con qué tratamientos hacéis para cada gestoría, los subencargados, las transferencias y las medidas de seguridad. Facilita RGPD ayuda a hacerlo.

**6. Plan de brechas.** Si se filtra algo, **avisáis a la gestoría sin dilación**. Según la guía de la AEPD, el plazo de aviso que fije el contrato «debe ser inferior a 72 horas en cualquier caso»; 24-48 horas es lo práctico. Ella tiene **72 horas** para notificar a la AEPD ([AEPD](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/brechas-de-datos-personales-notificacion)). El plan, en una página: quién decide, cómo se corta el acceso, cómo se avisa y qué se apunta. Conviene ensayarlo una vez.

**7. Evaluación de impacto (EIPD).** ✅ Verificado el 05-11-2026: la hace **el responsable, es decir, la gestoría**. El modelo de contrato de la AEPD solo os pide ayudarla con la información técnica. La lista de la AEPD usa criterios como gran escala o uso de IA, y con dos o más lo habitual es hacerla. Con unas pocas gestorías probablemente no aplica, pero conviene revisarlo al crecer, porque la IA ya es uno de esos criterios.

**8. Delegado de protección de datos.** ✅ Verificado el 05-11-2026: el art. 34 de la LOPDGDD **no incluye gestorías ni proveedores de software**. Queda por leer el art. 37.1 del RGPD, que es el criterio general, para descartarlo del todo.

**9. Qué saben los clientes de la gestoría.** Es la gestoría quien les informa de que usa proveedores. Conviene darle un texto breve que pueda añadir a su información de privacidad.

**10. Usar lo aprendido para mejorar el sistema.** Que lo que aprende una gestoría mejore el núcleo común necesita una **cláusula en el contrato**, y solo con reglas **sin datos personales** (sin NIF ni nombres).

**11. Responsabilidad por errores.** Si el sistema propone una cuenta mala y la gestoría la importa, ¿quién responde? Las condiciones del servicio deben dejar claro que **siempre revisa una persona antes de importar en Sage**, y limitar vuestra responsabilidad. Un **ciberseguro** (desde unos 350 €/año, fuente comercial: [blogthinkbig](https://blogthinkbig.com/ciberseguro-empresas)) cubre brechas y reclamaciones.

**12. Datos de prueba.** En el servidor de juguete, en preproducción, en las demos y en los chats con Claude, **solo datos inventados**. Nunca facturas reales de clientes del despacho.

**Abogado o plantillas:**
- **Piloto por Drive (Toro, padre de Alfredo):** basta con la plantilla de contrato hecha con las directrices de la AEPD, adaptada a cada gestoría, más la lista de subencargados.
- **Servidor abierto a gestorías desconocidas:** revisión por un profesional antes. La adecuación cuesta desde unos 800 € ([Legiscope](https://www.legiscope.com/blog/cuanto-cuesta-cumplir-rgpd.html)).

**Lo que no hace falta:** el ENS solo es obligatorio para el sector público y sus proveedores, no para trabajar con gestorías privadas.

## 6. Qué queda por verificar (actualizado el 05-11-2026)

Verificado desde el Mac el 05-11-2026: la autorización de subencargados, el plazo de aviso de brechas, los límites de Facilita, el delegado de protección de datos (art. 34 LOPDGDD) y quién hace la EIPD. Ya están en el apartado 5. **La recomendación sigue en pie.**

| Qué falta | Dónde | Estado |
|---|---|---|
| Stock real de los CX33/CX43: una lectura de la web los da como «no disponibles» | Consola de Hetzner | ⚠️ Comprobar antes de contar con ellos. **Plan B: OVH VPS-2, 7,21 € sin IVA** |
| Si el ENS Alto de OVH cubre los VPS | OVHcloud | Pedir el certificado |
| Precio de Haiku 5.5 en Bedrock UE, el +10 % regional y el acceso de la cuenta | AWS | Sin confirmar (la web dio error) |
| Lista de subencargados de Mistral: algunas funciones se procesan fuera de la UE | Mistral | Revisar |
| Object Lock de Scaleway; si su ISO 27001 cubre los Mac (solo si algún día hace falta Mac) | Scaleway | Sin confirmar (la web dio error) |
| Art. 37.1 del RGPD (criterio general del delegado) | EUR-Lex | Leer |
| Si las 72 horas de la AEPD cuentan festivos | AEPD | Sin confirmar |
