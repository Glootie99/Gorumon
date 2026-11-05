# Seguridad mínima y papeleo RGPD mínimo para una SaaS multi-tenant de facturas (gestorías), España, nov. 2026

Contexto: startup de 2 personas en España; SaaS multi-tenant que procesa facturas con datos personales por cuenta de gestorías. Las gestorías son **responsables del tratamiento** y la startup es **encargada del tratamiento** (art. 28 RGPD). Fecha de investigación: 2026-11-05.

Notas de método:
- **www.aepd.es no se podía abrir con WebFetch en esta sesión** (error ENOTFOUND: el dominio está fuera de la red permitida de la sesión). Todo el contenido de la AEPD viene de fragmentos de WebSearch más las URL oficiales. Para leer los PDF completos, hay que permitir www.aepd.es en la configuración de red de la sesión.
- Fuentes marcadas **[COMERCIAL]**: blogs de vendedores, agregadores de precios o páginas de proveedores. Las cifras en USD no se han convertido.
- Las URL de documentación de herramientas marcadas "(doc oficial, no abierta en esta sesión)" son las páginas oficiales del proyecto, citadas como referencia. No se verificaron en esta sesión.
- Esto no es asesoramiento jurídico. Resume la guía oficial y los precios publicados.

---

## 1. Marco legal mínimo: contrato art. 28, subencargados, RAT, EIPD, DPD

### Takeaway
Como encargada, la startup necesita al menos: (a) un contrato de encargo art. 28.3 (DPA) con cada gestoría, adaptado al caso y no genérico; (b) una lista de subencargados (hosting, backups, email, Cloudflare...) con nombre, dirección, contacto y tratamiento; (c) un registro de actividades como encargado (art. 30.2), más breve que el del responsable; (d) un procedimiento de brechas que avise al responsable "sin dilación indebida". Probablemente no está obligada a nombrar DPD (no figura en la lista del art. 34 LOPDGDD) y probablemente no necesita EIPD propia, aunque conviene evaluarlo con la lista de la AEPD. La EIPD es obligación del responsable, y el encargado debe ayudarle (art. 28.3.f).

### Cited Findings
**Contrato de encargo (art. 28)**
- La AEPD publicó, junto con la Autoritat Catalana de Protecció de Dades y la Datuak Babesteko Euskal Bulegoa, unas "Directrices para la elaboración de contratos entre responsables y encargados del tratamiento" (PDF oficial) — [AEPD guía directrices contratos](https://aepd.es/guias/guia-directrices-contratos.pdf)
- La AEPD también publica un documento de cláusulas tipo de encargado — [AEPD cláusulas contratos encargado](https://www.aepd.es/documento/clausulas-contratos-encargado-tratamiento.pdf). Su FAQ sobre el contenido del contrato remite a esas directrices — [AEPD FAQ-0238](https://www.aepd.es/preguntas-frecuentes/2-tus-obligaciones-como-responsable-del-tratamiento/8-responsable-y-encargado-del-tratamiento/FAQ-0238-cual-seria-el-contenido-del-contrato-de-encargo-de-tratamiento)
- Contenido mínimo según el art. 28.3: objeto y duración, naturaleza y finalidad, tipo de datos y categorías de interesados, entre otros — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/articulo-28-rgpd-obligaciones.html)
- La AEPD ha sancionado contratos genéricos que solo reproducen el RGPD sin adaptarlo al caso — [Fieldfisher [COMERCIAL/despacho]](https://www.fieldfisher.com/es-es/locations/spain/insights/mala-gestion-multa)
- INCIBE tiene un artículo divulgativo sobre qué debe contener el contrato de tratamiento — [INCIBE blog](https://www.incibe.es/empresas/blog/debe-contener-contrato-tratamiento-datos-personales)
- La Guía 7/2020 del CEPD/EDPB sobre responsable y encargado trata el nivel de detalle de las cláusulas — [Hogan Lovells [despacho]](https://www.hoganlovells.com/es/publications/nueva-guia-del-comite-europeo-de-proteccion-de-datos-sobre-coresponsable-y-encargado-bajo-el-rgpd)

**Lista de subencargados (EDPB Opinion 22/2024)**
- Según el EDPB, el responsable debe tener siempre disponible la identidad de toda la cadena de encargados y subencargados (nombre, dirección, persona de contacto, descripción del tratamiento). Es más estricto que la práctica habitual de listar solo el primer nivel — [IAPP](https://iapp.org/news/a/controllers-processors-and-subprocessors-in-chains); [Goodwin [despacho]](https://www.goodwinlaw.com/en/insights/blogs/2024/10/latest-edpb-opinion-what-you-need-to-know-about-using-processors-and-sub-processors)
- El encargado debe informar proactivamente al responsable de los subencargados que contrata. El deber de verificar las "garantías suficientes" se aplica a toda la cadena, sea cual sea el riesgo — [Mondaq](https://www.mondaq.com/unitedstates/data-protection/1534172/latest-edpb-opinion-what-you-need-to-know-about-using-processors-and-subprocessors); [Hunton](https://huntonak.com/privacy-and-information-security-law/edpb-adopts-opinion-on-processors-and-guidelines-on-legitimate-interests)
- Las fuentes no coinciden en la fecha de adopción (7, 9 u 17 de octubre de 2024). Hay que comprobarla en edpb.europa.eu — [HSF Kramer](https://www.hsfkramer.com/notes/data/2024-posts/EDPB-Opinion--How-far-down-the-supply-chain-do-controller-duties-extend--)

**Registro de actividades (RAT)**
- El registro del encargado (art. 30.2) es más breve: identifica a las partes y las categorías de tratamientos hechos por cuenta de cada responsable. Es de uso interno y debe estar a disposición de la AEPD — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/registro-actividades-tratamiento.html)
- La excepción del art. 30.5 (menos de 250 empleados) se interpreta de forma restrictiva y decae si el tratamiento no es ocasional. Por eso casi toda pyme debe llevar el RAT — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/registro-actividades-tratamiento.html); entrada del blog de la AEPD — [AEPD blog: Elaborar el RAT](https://www.aepd.es/prensa-y-comunicacion/blog/elaborar-el-registro-de-actividades-de-tratamiento)

**EIPD (DPIA)**
- La AEPD publica la "Lista de tipos de tratamientos de datos que requieren EIPD (art. 35.4)" — [AEPD PDF listas DPIA 35.4](https://www.aepd.es/documento/listas-dpia-es-35-4.pdf). También publica una lista orientativa de tratamientos que no la requieren (art. 35.5) — [AEPD Evaluaciones de impacto](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/evaluaciones-de-impacto)
- La lista recoge 11 tipos de tratamiento. En la mayoría de los casos la EIPD es necesaria cuando se cumplen dos o más criterios — [Osborne Clarke [despacho]](https://www.osborneclarke.com/es/insights/la-agencia-espanola-de-proteccion-de-datos-publica-la-lista-de-tratamientos-de-los-que-es-probable-que-entrane-un-alto-riesgo-y-precise-una-evaluacion-de-impacto-relativa-la-proteccion-de-datos); [PwC Periscopio](https://periscopiofiscalylegal.pwc.es/la-aepd-publica-un-listado-de-tratamientos-de-datos-que-requieren-evaluacion-de-impacto/)
- FAQ de la AEPD sobre cuándo es necesaria — [AEPD FAQ-0226](https://www.aepd.es/preguntas-frecuentes/2-tus-obligaciones-como-responsable-del-tratamiento/10-evaluacion-de-impacto/FAQ-0226-en-que-supuestos-es-necesario-realizar-una-evaluacion-de-impacto)

**DPD/DPO**
- El art. 34 de la LOPDGDD añade a los supuestos del art. 37 RGPD una lista de entidades obligadas: colegios profesionales, centros docentes, entidades de crédito y financieras, aseguradoras, empresas de seguridad, sanidad, telecomunicaciones, energía, etc. — [AEPD Designación DPD](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/delegado-de-proteccion-de-datos); [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/delegado-proteccion-datos.html)
- Una entidad que no encaja en el art. 34 LOPDGDD ni en el art. 37 RGPD no está obligada, aunque se recomienda nombrarlo voluntariamente — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/delegado-proteccion-datos.html)
- Precio orientativo de un DPD externo: 150–600 €/mes — [Legiscope "cuánto cuesta cumplir RGPD" [COMERCIAL]](https://www.legiscope.com/blog/cuanto-cuesta-cumplir-rgpd.html)

### Inferences
- Las gestorías no figuran en la lista del art. 34 en los fragmentos vistos (sí los colegios profesionales). Una SaaS pequeña de facturas probablemente no trata datos "a gran escala" en el sentido del art. 37.1, así que el DPD probablemente no es obligatorio. Hay que confirmarlo con el texto del BOE: a verificar.
- Las facturas contienen datos identificativos y económicos, no categorías especiales (art. 9). Con pocos clientes, es probable que no se cumplan dos criterios de la lista 35.4. Pero el criterio "gran escala", el uso de OCR/IA o la elaboración de perfiles podrían cambiarlo. La EIPD corresponde a cada gestoría como responsable, y el encargado debe darle la información técnica. A verificar con la lista oficial (no se pudo abrir).
- Paquete documental mínimo realista: plantilla de DPA (basada en las directrices de la AEPD), anexo de medidas de seguridad (art. 32), anexo de subencargados con el procedimiento de aviso previo y objeción, RAT como encargado, procedimiento de brechas, política de retención y borrado al terminar el contrato, y el RAT/cláusulas propias como responsable (empleados, leads, web).

### Gaps
- No se pudo leer la lista de 11 supuestos de la AEPD ni el texto literal del art. 34 LOPDGDD (aepd.es bloqueado; no se abrió el BOE).
- No hay un pronunciamiento oficial claro de que la excepción del art. 30.5 se aplique igual a los encargados.

---

## 2. Herramientas y guías oficiales gratuitas (AEPD, INCIBE, ENS)

### Takeaway
La AEPD ofrece gratis Facilita RGPD (riesgo bajo; genera RAT, cláusulas y cláusulas de encargado), Facilita EMPRENDE (startups tecnológicas) y Gestiona RGPD (análisis de riesgos, para responsables y encargados). INCIBE publica guías y políticas de seguridad para pymes, entre ellas una de relación con proveedores y otra de cloud.

### Cited Findings
- Facilita RGPD es gratuita, para tratamientos de escaso riesgo. Genera el RAT, cláusulas informativas y cláusulas contractuales para encargados. No sirve para alto riesgo (salud, tratamientos masivos). La AEPD dice que los datos introducidos se borran al terminar — [AEPD Facilita RGPD](https://www.aepd.es/guias-y-herramientas/herramientas/facilita-rgpd)
- Facilita EMPRENDE se dirige a startups y empresas con tecnologías innovadoras que no encajan en Facilita RGPD — [AEPD Facilita EMPRENDE](https://www.aepd.es/guias-y-herramientas/herramientas/facilita-emprende)
- Gestiona RGPD es un asistente más completo de gestión de tratamientos y riesgos, para responsables y encargados — [AEPD nota de prensa Gestiona RGPD](https://www.aepd.es/prensa-y-comunicacion/notas-de-prensa/aepd-lanza-nueva-version-gestiona-rgpd)
- La AEPD tiene una página de orientación a pymes — [AEPD Pymes](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/directrices-de-aplicacion/pymes)
- Facilita RGPD superó el millón de descargas — [AEPD prensa](https://www.aepd.es/prensa-y-comunicacion/facilita-rgpd-alcanza-millon-de-descargas)
- INCIBE: índice de guías para empresas, sección sobre seguridad en la nube y políticas de seguridad para pymes (relación con proveedores, concienciación) — [INCIBE guías](https://www.incibe.es/empresas/guias); [INCIBE seguridad en la nube](https://www.incibe.es/empresas/blog/tematicas-seguridad-nube); [INCIBE política concienciación (PDF)](https://www.incibe.es/sites/default/files/contenidos/politicas/documentos/concienciacion-y-formacion.pdf)
- Un blog comercial sostiene que con encargados, salud o marketing hace falta una solución de pago. Es opinión de un vendedor, no criterio de la AEPD — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/software-rgpd-pymes.html)

### Inferences
- Facilita RGPD o Facilita EMPRENDE más las directrices de contratos de la AEPD pueden producir un primer borrador de RAT y DPA a coste 0 €. Una revisión profesional después reduce el coste del abogado.
- ENS (RD 311/2022, CCN-CERT) solo es obligatorio para el sector público y sus proveedores. Para clientes privados como las gestorías sirve como marco de referencia de medidas, no como obligación. Esto no se verificó en esta sesión: a verificar.

### Gaps
- No se buscaron guías CCN-STIC concretas (por ejemplo, perfiles de cumplimiento ENS para pymes o la serie CCN-STIC 800). Tampoco se confirmó si existe la "guía de seguridad de la información para encargados".

---

## 3. Plan de incidentes y brechas (72 h AEPD; encargado → responsable sin dilación)

### Takeaway
El responsable (la gestoría) notifica a la AEPD en 72 h desde que tiene constancia, fines de semana y festivos incluidos. El encargado (la startup) debe avisar al responsable sin dilación indebida con todos los detalles relevantes. Puede notificar a la AEPD en nombre del responsable si el contrato lo prevé. La notificación puede hacerse por fases, y se presenta por la Sede Electrónica.

### Cited Findings
- Plazo de 72 h desde la constancia de la brecha. La guía actualizada en 2021 aclara que incluye fines de semana y festivos — [AEPD Notificación de brechas](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/brechas-de-datos-personales-notificacion); [finreg360](https://finreg360.com/alerta/la-aepd-actualiza-la-guia-para-la-notificacion-de-brechas-de-datos-personales/)
- El encargado debe comunicar la brecha al responsable sin dilación indebida, con todos los detalles relevantes. Puede notificar a la AEPD en nombre del responsable si el contrato lo establece: una notificación por responsable, o una sola para hasta 10 responsables afectados por igual — [AEPD Notificación de brechas](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/brechas-de-datos-personales-notificacion)
- La notificación puede ser gradual: una inicial dentro de las 72 h y luego información complementaria. Se presenta por el formulario de la Sede Electrónica — misma fuente
- Guía oficial: "Guía para la Gestión y Notificación de Brechas de Datos Personales" (junio 2021) — [AEPD](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/brechas-de-datos-personales-notificacion); FAQ — [AEPD FAQ-0233](https://www.aepd.es/preguntas-frecuentes/2-rgpd/11-brechas-de-datos-personales/FAQ-0233-a-quien-hay-que-notificar-las-brechas-de-datos-personales)
- Fuente no oficial: si la brecha la sufre el encargado, el plazo del responsable empieza cuando el encargado se lo comunica — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/notificar-brecha-seguridad-aepd.html) (a verificar en la guía oficial)

### Inferences
- Plan mínimo (1–2 páginas): roles (quién decide, quién comunica), contactos de cada gestoría, plantilla de aviso al responsable (qué pasó, cuándo, datos y tenants afectados, medidas, contacto), un registro interno de todas las brechas (también las no notificadas, art. 33.5), preservación de logs, y un simulacro anual. Conviene fijar en el DPA un plazo concreto (por ejemplo, 24–48 h) para que la gestoría pueda cumplir sus 72 h. La cifra es una práctica de mercado, no una exigencia de la AEPD.
- Coste: 0 € (tiempo interno).

### Gaps
- No se pudo leer el texto completo de la guía de 2021 ni comprobar si hay una versión posterior a 2021.

---

## 4. Controles técnicos mínimos en VPS Linux (o híbrido con Mac): qué es, cómo, herramientas y coste

### Takeaway
Casi todos los controles se pueden cubrir con software libre a 0 € de licencia sobre un VPS. Los costes recurrentes reales son: hosting (fuera de este alcance), un destino de backup externo (por ejemplo, Hetzner Storage Box 1 TB a unos 3,20 €/mes sin IVA), Cloudflare (Free a 0 €, o Pro a 20 $/mes anual o 25 $/mes mensual) y, de forma opcional, monitorización o secretos SaaS (hay capas gratuitas). Cloudflare Zero Trust/Access es gratis hasta 50 usuarios.

### Cited Findings (precios)
- **Cloudflare Zero Trust (Access, Tunnel):** plan Free a 0 $ para menos de 50 usuarios. Pay-as-you-go a 7 $/usuario/mes (anual). Las fuentes no coinciden en la retención de logs del plan Free (24 h según terceros) — [Cloudflare plans SASE/Zero Trust (oficial)](https://www.cloudflare.com/plans/sase-zero-trust.md); [costbench [COMERCIAL]](https://costbench.com/software/business-vpn/cloudflare-zero-trust/free-plan/); [controld [COMERCIAL]](https://controld.com/blog/cloudflare-zero-trust-pricing/)
- **Cloudflare Pro:** 20 $/mes facturado anualmente o 25 $/mes mensual, por dominio. Incluye las reglas WAF gestionadas (OWASP); los conjuntos más amplios y el SLA van en Business, a unos 200 $/mes. Una fuente aislada dice que el precio subió a 25 $ en 2026. A verificar en cloudflare.com/plans — [eastondev [COMERCIAL]](https://eastondev.com/blog/en/posts/dev/20251201-cloudflare-pricing-compare/); [activepieces [COMERCIAL]](https://www.activepieces.com/blog/cloudflare-pricing-2026-plans-and-what-you-pay); [blazingcdn [COMERCIAL]](https://blog.blazingcdn.com/en-us/cloudflare-pricing-2026-free-pro-business-enterprise-explained)
- **Hetzner Storage Box BX11 (1 TB):** unos 3,20 €/mes sin IVA (agregadores con fecha oct. 2025 y jun. 2026). No se confirmó en hetzner.com — [Hetzner BX11 (oficial)](https://www.hetzner.com/de/storage/storage-box/bx11); [cloud-cost aggregator [COMERCIAL]](https://cloud-cost-557.pages.dev/provider/hetzner/); [whtop [COMERCIAL]](https://www.whtop.com/compare/hetzner,webtropia)
- **Better Stack Uptime:** capa gratuita de unos 10 monitores con chequeo cada 3 min (algunas fuentes dicen 2 min, 5 o 3 monitores). El plan de pago "Responder" cuesta unos 29 $/mes anual. Las cifras no coinciden: a verificar en betterstack.com/pricing — [devtoollab [COMERCIAL]](https://devtoollab.com/blog/best-uptime-monitoring-tools); [devtoolpicks [COMERCIAL]](https://devtoolpicks.com/blog/best-uptime-monitoring-tools-indie-hackers-2026); [Better Stack comparativa (vendedor)](https://betterstack.com/community/comparisons/uptime-robot-alternatives.md)
- **Infisical:** capa gratuita de 5 identidades, 3 proyectos y 3 entornos, también autoalojable. Pro desde 18 $/identidad/mes — [costbench [COMERCIAL]](https://www.costbench.com/software/secrets-management/infisical/); [toolradar [COMERCIAL]](https://toolradar.com/tools/infisical/pricing)
- **Doppler:** las fuentes no coinciden. Unas citan un plan Developer gratuito de hasta 3 usuarios y luego 8 $/usuario/mes, más un plan Team a 21 $/usuario/mes. Otra (costbench, jun. 2026) dice que no hay plan gratuito. A verificar — [merginit [COMERCIAL]](https://merginit.com/blog/23062026-free-secrets-env-management-comparison); [costbench Doppler [COMERCIAL]](https://costbench.com/software/developer-tools/doppler-dev/free-plan/)

### Notas por control (implementación de bajo coste)
Las herramientas citadas son software libre (licencia 0 €). Documentación oficial citada como referencia, no abierta en esta sesión.

1. **HTTPS/TLS y cifrado en reposo.** TLS: Caddy (certificados automáticos de Let's Encrypt) o Nginx con certbot. Si se usa Cloudflare, el modo "Full (strict)" con un certificado de origen. Disco: LUKS en el volumen de datos (en un VPS suele exigir desbloqueo remoto, por ejemplo con dropbear-initramfs) o cifrado del volumen por el proveedor. BD: PostgreSQL no tiene TDE nativo en la versión comunitaria, así que se combina cifrado de disco con cifrado de campos sensibles en la aplicación. Claves por tenant: envelope encryption (una DEK por tenant, cifrada con una KEK guardada en sops/age, Vault o Infisical). Permite el "crypto-shredding" al dar de baja a un tenant. Backups: restic cifra siempre (AES-256). Refs: [Caddy docs](https://caddyserver.com/docs/automatic-https), [restic docs](https://restic.readthedocs.io/), [age](https://github.com/FiloSottile/age) (doc oficial, no abierta en esta sesión). Coste: 0 €.
2. **2FA y roles.** Autoalojado: Authentik, Keycloak, Zitadel (OIDC/SAML, TOTP/WebAuthn) o Authelia (proxy de autenticación ligero, ideal para paneles internos). Gestionado: Cloudflare Access delante de los paneles de administración (0 $ hasta 50 usuarios, ver arriba). Para los usuarios finales de las gestorías: 2FA TOTP/WebAuthn en la app o vía OIDC, con roles por tenant (admin de gestoría, usuario, solo lectura) y un superadmin interno separado. Refs: [authentik](https://goauthentik.io/), [Keycloak](https://www.keycloak.org/), [Zitadel](https://zitadel.com/), [Authelia](https://www.authelia.com/) (doc oficial, no abierta en esta sesión). Coste: 0 € autoalojado (consumo de RAM: Keycloak es el más pesado).
3. **Aislamiento de tenants.** Opciones de menor a mayor aislamiento: tenant_id con Row-Level Security de PostgreSQL; un schema por tenant; una BD por tenant. Almacenamiento: prefijo o bucket por tenant y URL firmadas de corta duración. Pruebas automáticas en CI: crear dos tenants e intentar acceder a recursos cruzados (IDOR), un test por endpoint. Ref: [PostgreSQL RLS](https://www.postgresql.org/docs/current/ddl-rowsecurity.html) (doc oficial, no abierta en esta sesión). Coste: 0 €.
4. **Backups 3-2-1 con prueba de restauración.** restic o borg (borg con borgmatic), cifrado de cliente. Copia 1 en el VPS, copia 2 en una Storage Box o S3 de otro proveedor, copia 3 offline en el Mac/NAS o en almacenamiento con object lock. pg_dump o pgBackRest para la BD. La restauración se prueba en un VPS efímero al menos cada trimestre, y se anota en un registro. age para cifrar los dumps sueltos. Coste: unos 3,20 €/mes (Storage Box BX11, ver arriba) más el disco local.
5. **Logs de auditoría que no se puedan borrar.** Tabla append-only (sin permisos UPDATE/DELETE para el rol de la app y con triggers), cadena de hashes, y envío en tiempo real fuera del VPS: syslog remoto, Loki, o un bucket S3 con Object Lock en modo compliance (WORM). auditd para el sistema. Coste: 0 € a unos pocos €/mes según el almacenamiento (a verificar con el proveedor S3 elegido).
6. **Parches y análisis de dependencias.** unattended-upgrades (Debian/Ubuntu) para los parches de seguridad, con reinicio programado o needrestart. Trivy para imágenes de contenedor, el sistema de ficheros y las IaC. pip-audit o npm audit en CI. Dependabot o Renovate en GitHub (gratis en repos de GitHub). Refs: [Debian UnattendedUpgrades](https://wiki.debian.org/UnattendedUpgrades), [Trivy](https://trivy.dev/), [pip-audit](https://github.com/pypa/pip-audit), [Dependabot](https://docs.github.com/code-security/dependabot) (doc oficial, no abierta en esta sesión). Coste: 0 €.
7. **Gestión de secretos.** Lo mínimo para 2 personas: sops + age (secretos cifrados en git, clave age en cada portátil y en el servidor). Alternativas: Infisical (capa gratuita o autoalojado), Doppler (precio no confirmado) y HashiCorp/OpenBao Vault (más pesado de operar). Coste: 0 €. Ref: [sops](https://github.com/getsops/sops) (doc oficial, no abierta en esta sesión).
8. **Exponer solo el front.** Firewall con ufw/nftables: denegar todo por defecto y abrir solo 443, o nada si se usa Cloudflare Tunnel (cloudflared). SSH solo por clave y por red privada o VPN (WireGuard, Tailscale) o Cloudflare Access. BD, Redis y paneles de administración en localhost o en la red privada. fail2ban o CrowdSec. WAF: reglas gestionadas de Cloudflare Pro (20–25 $/mes) o el Free con reglas básicas. Coste: 0 € a 25 $/mes.
9. **Subidas de ficheros seguras.** Límite de tamaño en el proxy y en la app. Lista blanca de tipos validada por magic bytes, no por extensión. Nombre aleatorio y almacenamiento fuera del webroot. Parseo de PDF/OCR en un worker aislado (contenedor sin red, usuario no root, seccomp, límites de CPU/RAM y timeout; opcionalmente gVisor/bubblewrap). Antivirus ClamAV (clamd) antes de procesar. Ref: [OWASP File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html), [ClamAV docs](https://docs.clamav.net/) (doc oficial, no abierta en esta sesión). Coste: 0 € (ClamAV usa del orden de 1 GB+ de RAM: a verificar).
10. **Plan de incidentes y brechas.** Ver la sección 3.
11. **Monitorización y alertas.** Uptime Kuma autoalojado (0 €; mejor alojarlo fuera del VPS vigilado, por ejemplo en el Mac o en un VPS mínimo) y/o la capa gratuita de Better Stack (unos 10 monitores, ver arriba). Alertas por email, Telegram o Slack. Ref: [Uptime Kuma](https://github.com/louislam/uptime-kuma) (doc oficial, no abierta en esta sesión).

### Inferences
- Coste mensual mínimo de los controles (sin el VPS): unos 3–4 €/mes (destino de backup) con Cloudflare Free, Access Free, Better Stack Free y sops/age. Si se añade Cloudflare Pro, unos 20–25 $/mes más.
- El documento "anexo de medidas de seguridad" del DPA puede listar exactamente estos 11 controles. Eso cubre a la vez el art. 28.3.c, el art. 32 y la diligencia que piden las gestorías.

### Gaps
- No se verificó en las páginas oficiales ningún precio de Cloudflare, Hetzner, Better Stack ni Doppler. Todos vienen de agregadores [COMERCIAL] y deben confirmarse ("a verificar").
- No se buscaron precios de S3 con Object Lock (Backblaze B2, Wasabi, Scaleway) para los logs WORM.

---

## 5. Pentest externo, revisión legal y ciberseguro: precios en España

### Takeaway
Pentest web pequeño en España: desde unos 1.490 € (alcance web/API muy acotado), con lo habitual entre 2.000 y 6.000 € para una web sencilla y entre 5.000 y 15.000 € para un alcance medio. Adecuación RGPD inicial: 800–15.000 € según complejidad. No se encontraron tarifas publicadas de abogados para revisar solo un DPA. Ciberseguro: "desde unos 350 €/año" según una fuente comercial. Las aseguradoras (Mapfre, Hiscox, Reale, Stoïk) no publican tarifa y hay que pedir presupuesto.

### Cited Findings
- **Pentest:** "desde 1.490 €" para un alcance web/API acotado. Web sencilla: 2.000–6.000 €. Web, API o entorno medio: 5.000–15.000 €. El precio sube con los perfiles de usuario, la lógica de negocio y las integraciones — [Hard2bit [COMERCIAL, proveedor español]](https://hard2bit.com/blog/cuanto-cuesta-un-pentesting-en-espana/)
- Referencias internacionales: pentest web de 5.000 $ a 30.000 $+; para startups, 5.000–15.000 $ (2026). Ningún test completo baja de unos 4.000 $; lo más barato suele ser solo un escaneo automático — [7ASecurity [COMERCIAL]](https://7asecurity.com/blog/2026/04/the-2026-guide-to-penetration-testing-pricing-and-scoping/); [Redfox [COMERCIAL]](https://www.redfoxsec.com/blog/how-much-does-web-application-penetration-testing-cost-2026-pricing-guide); [Astra [COMERCIAL]](https://www.getastra.com/blog/?p=15194)
- **Revisión RGPD:** adecuación inicial de 800–15.000 €, DPD externo de 150–600 €/mes, herramientas de 0 € a cuatro cifras (2026) — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/cuanto-cuesta-cumplir-rgpd.html). Software RGPD para pymes de 10–100 empleados: 1.500–6.000 €/año — [Legiscope [COMERCIAL]](https://www.legiscope.com/blog/precio-software-rgpd.html)
- Despachos como Andersen ofrecen adaptación RGPD y DPD externo sin precio publicado — [Andersen](https://es.andersen.com/esta-su-empresa-preparada-para-el-reglamento-europeo-de-proteccion-de-datos/)
- **Ciberseguro:** "pueden empezar en 350 euros anuales" — [blogthinkbig (Telefónica) [COMERCIAL]](https://blogthinkbig.com/ciberseguro-empresas). Para pequeñas empresas, desde unos cientos de euros al año hasta muchos miles para grandes empresas — [Xataka](https://www.xataka.com/pro/seguro-riesgos-ciberneticos-para-empresas-autonomos-que-que-amenazas-cubre-que-conviene-contratar-uno)
- Productos sin precio publicado: Mapfre Ciberriesgos — [Mapfre](https://www.mapfre.es/seguros/empresas/seguros-de-responsabilidad-civil/seguro-ciberriesgos/); Hiscox CyberClear 360 — [Hiscox folleto](https://www.hiscox.es/sites/spain/files/2022-11/Folleto%20corredor%20Hiscox%20CyberClear%20360%20-%20new.pdf); Reale Ciber 2.0 (IPID) — [Reale](https://www.reale.es/es/Documents/IPID.%20133%20-%20Reale%20Ciber%202.0.pdf); Stoïk (insurtech para pymes, llegó a España) — [Escudo Digital](https://www.escudodigital.com/empresas/stoik-insurtech-francesa-especializada-en-riesgos-ciberneticos-pymes-se-instala-en-espana.html)
- Coste medio de un ciberataque a una pyme: las cifras no coinciden (102.000 € frente a 35.000 €, según el Colegio de Mediadores), tomadas de resúmenes de prensa — [Xataka](https://www.xataka.com/pro/seguro-riesgos-ciberneticos-para-empresas-autonomos-que-que-amenazas-cubre-que-conviene-contratar-uno) (cifras de baja fiabilidad)

### Inferences
- Para una MVP de 2 personas, un pentest acotado (web, API y pruebas de aislamiento multi-tenant, 2–3 roles) caería previsiblemente en la franja de 1.500–6.000 €. Conviene pedir al menos 3 ofertas con el alcance cerrado, e incluir explícitamente las pruebas de acceso cruzado entre tenants.
- Revisión legal mínima (DPA, anexo de subencargados, RAT y textos legales de la web): no se encontró una tarifa publicada específica; a verificar con al menos 3 presupuestos. La franja baja del rango de Legiscope (unos 800 €) es la única referencia con cifra.
- Ciberseguro: prima a verificar con un corredor. La única cifra encontrada (unos 350 €/año como mínimo) es de una fuente comercial sin coberturas detalladas. Las aseguradoras suelen pedir 2FA, backups y parches, lo que coincide con la sección 4 (inferencia, no verificada).

### Gaps
- No se encontraron tarifas por hora ni por proyecto de abogados colegiados para revisar un DPA de SaaS.
- No hay prima concreta publicada por ninguna aseguradora española para una SaaS de facturación con unos 10–100 clientes.
- Los precios de pentest vienen de proveedores (sesgo comercial) y no se verificaron otras tarifas españolas.
