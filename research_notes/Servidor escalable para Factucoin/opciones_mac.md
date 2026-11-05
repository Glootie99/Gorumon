# Opciones Mac (Apple Vision OCR): Mac mini en casa (A), híbrido nube UE + Mac en casa (D), Mac alquilado en CPD UE (E). Notas a 5-nov-2026

Notas de método:
- WebFetch está bloqueado en este entorno para scaleway.com, apple.com y aws.amazon.com (DNS ENOTFOUND, 5-nov-2026). Todo procede de snippets de WebSearch. Para que sean definitivas, hay que verificar las cifras en las páginas oficiales.
- Casi todas las cifras proceden de agregadores o tiendas y se marcan como tales. "a verificar" significa que no se pudo confirmar en la fuente oficial.
- Impuestos: los precios de tiendas españolas incluyen IVA salvo que se indique otra cosa. Los precios de proveedores cloud no incluyen IVA.

## 1. Mac mini en casa (opción A): hardware, electricidad, SAI, conexión y backup

### Takeaway
En España, un Mac mini nuevo de la generación actual (lanzado el 22-sep-2026 y llamado "M6" por tiendas y prensa; la denominación está por verificar en apple.com/es) parte de unos 1.069 € con 16 GB y 256 GB. Con 16 GB y 512 GB ronda los 1.245-1.280 € en tiendas. Consume muy poco: según ENERGY STAR, unos 3 W en reposo, lo que da decenas de euros de luz al año. La fibra residencial española (Digi, 20-30 €/mes por 1 Gb, IP pública por +1 €/mes) basta en ancho de banda, pero tiene dos problemas: CG-NAT o IP dinámica y cláusulas de "uso residencial". Por eso conviene un túnel saliente (Cloudflare o Tailscale) en lugar de abrir puertos. Un SAI cuesta unos 90-115 € y un backup 4G/5G con SIM de datos ilimitados de Digi, unos 10-12 €/mes más el router.

### Cited Findings
**Precio del Mac mini en España (nuevo)**
- Mac mini de la generación actual ("M6" según la fuente) a la venta en España desde el 22-sep-2026, desde 1.069 €; versión educativa 949 €. Fuente: medio de tecnología (agregador), no Apple. Nombre del chip y precio a verificar en apple.com/es — [Hardmaniacos](https://www.hardmaniacos.com/mac-mini-m6-mac-studio-m5-ultra-disponibles-espana/)
- Refurb.me: M6 lanzado el 22-sep-2026 con un precio de salida de 1.069 € (agregador) — [Refurb.me](https://www.refurb.me/es/stats/mac-mini)
- Una tienda cita "desde 1.047 € (PVP Apple 1.069 €)". Ese PVP correspondería a M6/16 GB/256 GB según los snippets — [MacMan](https://macman.es/comprar/mac-mini/)
- M6 16 GB/512 GB: ShopDutyFree 1.279,74 € con IVA; MediaMarkt 1.244 €. Son precios de tienda, no PVP Apple — [ShopDutyFree](https://www.shopdutyfree.es/comprar-mac-mini-m6-16gb-512gb); [MediaMarkt](https://www.mediamarkt.es/es/brand/apple/mac/mac-mini)
- Xataka informa de que Apple eliminó el Mac mini de 256 GB "en plena crisis de RAM". Esto contradice que el modelo de 1.069 € tenga 256 GB, así que la configuración base está por verificar — [Xataka](https://www.xataka.com/ordenadores/apple-se-carga-mac-mini-256gb-plena-crisis-ram-su-ordenador-barato-era-chollo-demasiado-bueno-para-durar)
- Mac mini M5 Pro: PVP recomendado 2.019 € (K-tuin), en oferta a 1.899 €. Chollometro recoge ofertas desde 1.799,95 € (oct-2026) — [K-tuin](https://www.k-tuin.com/mac-mini-m5-pro-24gb-512gb); [Chollometro](https://www.chollometro.com/categorias/mac-mini)
- Comparativa de Xataka entre los nuevos Mac mini M6 y M5 Pro y los modelos de 2024 — [Xataka](https://www.xataka.com/seleccion/identicos-fuera-diferentes-dentro-ponemos-frente-a-frente-nuevos-mac-mini-m6-m5-pro-modelos-2024)
- PRECIOS ANTIGUOS (generación M4, 2024-2025): el Mac mini M4 salió por 719 € (16 GB/256 GB), dato de hace más de 2 años; el M4 con 16 GB/512 GB, unos 949 €; el M4 Pro 12C/16G, 1.669 € (PVP 2024). Sirven solo como referencia del mercado de segunda mano o restos de stock — [Chollometro](https://www.chollometro.com/categorias/mac-mini); [PcComponentes blog](https://www.pccomponentes.com/blog/mac-mini-2024-m4-analisis-especificaciones-precio); [EveryMac](https://everymac.com/global-mac-prices/all-msrp-mac-mini-prices-in-spain.html)
- Mac mini M4 reacondicionado en Amazon Renewed España: 16 GB/512 GB por 1.256 €; 24 GB/512 GB por 1.106 €. Las cifras son incoherentes entre sí (agregador) — [Refurb.me](https://www.refurb.me/es/refurbished/mac-mini/by-amazon)
- No obtuve el precio oficial de las ampliaciones de RAM (24 o 32 GB) en Apple España: a verificar.

**Consumo eléctrico**
- ENERGY STAR (oficial), Mac mini M4 A3238: reposo corto 3,3 W, reposo largo 2,9 W, suspensión 0,8 W, apagado 0,1 W (ficha capturada el 15-jun-2026) — [ENERGY STAR](https://www.energystar.gov/productfinder/product/certified-computers/details/4513879)
- Medidas de terceros: ServeTheHome, 4-6 W en reposo; Jeff Geerling, unos 3 W (M4 base 16 GB) y unos 3,5 W (M4 Pro) — [ServeTheHome](https://servethehome.com/the-apple-mac-mini-m4-sets-the-mini-computer-standard/3); [Jeff Geerling](https://jeffgeerling.com/node/3419)
- No encontré cifras fiables de consumo a plena carga en estos resultados. No hay datos del M6.

**Precio de la electricidad en España (2026)**
- PVPC, término de energía sin impuestos (Selectra, medio privado, no oficial): media de octubre de 2026 de unos 0,196-0,199 €/kWh; septiembre de 2026, 0,184; agosto de 2026, 0,166. Las medias diarias de octubre fueron de 0,144 a 0,240 €/kWh — [Selectra 31-oct-2026](https://selectra.es/energia/noticias/precio-luz/2026-10-31); [Selectra 27-oct-2026](https://selectra.es/energia/noticias/precio-luz/2026-10-27)
- No encontré datos de la OCU ni de OMIE/REE (esios). Las cifras oficiales están por verificar.

**SAI**
- Salicru SPS 650 SOHO+: 90,50 €; APC Back-UPS 650VA: 112,10 € (tiendasigloxxi.es, snapshot sin fecha) — [tiendasigloxxi Salicru](https://tiendasigloxxi.es/en/power-bank/122699-ups-salicru-sps-700-one-bl-iec-8436584874980.html); [tiendasigloxxi APC](https://tiendasigloxxi.es/en/power-bank/129091-apc-back-ups-650va-230v-1usb-charging-0731304347194.html)
- Salicru SPS 700 ONE BL: 57,58 € sin IVA (snapshot) — [tiendasigloxxi](https://tiendasigloxxi.es/en/power-bank/122699-ups-salicru-sps-700-one-bl-iec-8436584874980.html); también en [MediaMarkt](https://www.mediamarkt.es/es/product/_sai-salicru-sps-700-one-bl-153374733.html) (precio a verificar)

**Fibra doméstica (Digi como referencia)**
- Web oficial de Digi: Fibra SMART 1 Gb por 20 €/mes; Fibra 1 Gb por 30 €/mes (sobre red de Movistar/NEBA) — [Digi](https://www.digimobil.es/fibra-optica/)
- Digi anunció que no sube precios en 2026 — [Vozpópuli](https://www.vozpopuli.com/economia/telecomunicaciones/digi-reta-a-telefonica-masorange-y-vodafone-y-descarta-subir-precios-en-2026.html)
- CG-NAT: las fuentes se contradicen. Una dice "IP pública dinámica, sin CG-NAT"; otra, "CG-NAT incluido, +1 €/mes por IP pública". Digi ofrece "Conexión Plus" (IP pública) por 1 €/mes. Los comparadores no son documentación técnica — [Kompara](https://kompara.es/internet/precio/fibra-mas-barata-espana-hoy); [Bandaancha](https://bandaancha.eu/articulos/tarifas/2)
- Según comparativas, O2 y Lowi no usan CG-NAT e incluyen IP pública — [Kompara](https://kompara.es/internet-movil/tarifas/digi-vs-lowi-comparativa)
- No confirmé la velocidad de subida simétrica de Digi 1 Gb: a verificar.

**Condiciones de uso (ToS)**
- Ejemplo de contrato de fibra español (operador no identificado, alojado en web de cooperativa): prohíbe expresamente "la instalación de servidores (webservers, FTP servers, mail servers etc.)" y define el servicio como "exclusivamente RESIDENCIAL" — [Condiciones cooperativa](https://www.marianoacosta.coop/wp-content/uploads/2019/10/Condiciones-Particulares-y-Generales-WEB.pdf)
- Olin: servicio "únicamente para uso particular en el domicilio" — [Olin](https://olin.es/wp-content/uploads/2023/04/CONDICIONESGENERALESCONTRATACIONFIBRAV21680684337-1.pdf)
- Movistar (condiciones de 2022, ANTIGUAS): "abstenerse de cualquier uso no contemplado en este contrato", sin mención explícita a servidores en el extracto — [Movistar CCPP 2022](https://www.movistar.es/rpmm/estaticos/residencial/fijo/HISTORICO/historico2022/condiciones-particulares-movistar-conecta-600_hasta-280822.pdf)
- No encontré el texto vigente de Digi ni de Movistar sobre servidores.

**Backup 4G/5G**
- Digi, datos ilimitados 5G: unos 10 €/mes sin IVA, unos 12,10 € con IVA (comparadores, may-2026) — [Roams](https://roams.es/companias-telefonicas/digimobil/guias/telefonia/datos-ilimitados/); [Kompara](https://kompara.es/movil/precio/digi)
- Referencia de operadores tradicionales con router: Vodafone Internet Portátil 5G a unos 30 €/mes y Orange Internet 5G en casa a unos 35 €/mes (cifra única sin contrastar) — [Kompara](https://kompara.es/movil/precio/sim-movil-en-router-4g-tablet)
- No obtuve el precio de un router 4G/5G con failover: a verificar.

### Inferences
- Electricidad (cálculo propio con las cifras anteriores): con una media de 10 W, el consumo es de unos 88 kWh/año; con 30 W, de unos 263 kWh/año. Al PVPC de oct-2026 (unos 0,20 €/kWh, energía sin impuestos ni peaje de potencia) salen unos 18-53 €/año, más impuestos (IVA e impuesto eléctrico). En cualquier caso, menos de unos 70 €/año. La carga real de OCR determina dónde se cae dentro de ese rango.
- Ancho de banda: las facturas en PDF o imagen ocupan del orden de cientos de KB a pocos MB. Incluso 30 gestorías en semana de cierre caben en cualquier fibra de 300 Mb o más. El cuello de botella es la disponibilidad (cortes de luz o de fibra, reinicios del router, CG-NAT), no la velocidad.
- Coste de capital de A (estimado): Mac mini (unos 1.069-1.280 €) + SAI (unos 90-115 €) + router 4G con SIM (unos 12 €/mes + router a verificar). Amortizado a 3 años, sale por unos 35-45 €/mes más una fibra que probablemente ya se paga.
- Por las cláusulas de "uso residencial" y servidores, exponer un SaaS B2B desde una línea doméstica puede incumplir el contrato. Una línea de empresa (autónomo/pyme) o el patrón D, con solo conexiones salientes, reducen ese riesgo.

### Gaps
- PVP oficial de Apple España para cada configuración y para las ampliaciones de RAM (24/32 GB) del modelo actual (apple.com bloqueado).
- Consumo a carga sostenida de OCR del Mac mini actual.
- Datos oficiales de OMIE/REE y de la OCU sobre el precio de la luz en 2026.
- Subida real y CG-NAT de Digi, y cláusulas vigentes de servidores en Digi, Movistar, O2 y Vodafone.

## 2. Exposición segura sin abrir puertos: Cloudflare Tunnel vs Tailscale (Funnel) vs WireGuard

### Takeaway
Cloudflare Tunnel y Tailscale Funnel evitan abrir puertos y sortean el CG-NAT, pero con un modelo de confianza distinto. Cloudflare termina el TLS en su edge, así que ve el contenido en claro. Mantener la terminación TLS solo en la UE (Regional Services, dentro de la Data Localization Suite) es una opción de pago reservada a Enterprise. En Tailscale Funnel, en cambio, el TLS termina en tu dispositivo y el relay no puede descifrar. Los relays DERP solo ven paquetes WireGuard cifrados y metadatos de quién habla con quién. El plan gratuito de Tailscale es para uso no comercial. Ambas son empresas de EE. UU.

### Cited Findings
**Cloudflare Tunnel**
- Tunnel disponible en todos los planes, incluido el gratuito (guía de terceros) — [comptech-lab](https://comptech-lab-blog.pages.dev/learn/cloudflare/cloudflare-tunnel)
- Cloudflare termina el TLS en su edge (guía de terceros) — [selfhosted-sh](https://selfhosted-sh.pages.dev/cloudflare-tunnels-zero-trust-access)
- Docs de Cloudflare: con Regional Services, el TLS "solo se termina dentro de la región configurada". Forma parte de la Data Localization Suite — [Cloudflare Docs DLS FAQ](https://developers.cloudflare.com/data-localization/faq)
- La DLS es de pago y solo para Enterprise; no está disponible en los planes Free, Pro ni Business (guía francesa de cumplimiento) — [donneespersonnelles.fr](https://donneespersonnelles.fr/cloudflare-rgpd)
- La FAQ de Cloudflare afirma que sus servicios están diseñados para cumplir el RGPD incluso sin DLS — [Cloudflare Docs](https://developers.cloudflare.com/data-localization/faq)
- En el plan gratuito hay que usar el certificado que proporciona Cloudflare (foro de Nextcloud; la opinión sobre privacidad es de un usuario) — [Nextcloud forum](https://help.nextcloud.com/t/is-cloudflare-tunnel-safe-privacy-focused/150268)

**Tailscale / Funnel**
- Docs de Funnel: "el servidor relay de Funnel no puede descifrar los datos"; el TLS lo termina el Tailscale de tu dispositivo. Funnel solo escucha en los puertos 443, 8443 y 10000, solo admite TLS y tiene "límites de ancho de banda no configurables" (sin cifras publicadas en los snippets) — [Tailscale Funnel docs](https://tailscale.com/kb/1223/tailscale-funnel)
- Cifrado: el plano de control gestiona coordinación, autenticación y ACL; los relays DERP "nunca acceden a tus datos sin cifrar", solo a paquetes WireGuard ya cifrados — [Tailscale encryption](https://tailscale.com/kb/1504/encryption)
- Un relay sí ve qué nodo habla con cuál (metadatos) — [Starmorph](https://blog.starmorph.com/blog/tailscale-complete-developer-reference-guide)
- Precios (agregadores; las cifras de usuarios se contradicen): Personal gratuito para uso NO comercial, hasta 6 usuarios según fuentes de 2026 (3 en fuentes antiguas); Standard 8 $/usuario/mes; Premium 18 $/usuario/mes. Serve y Funnel no tienen coste añadido, solo restricción por política (ACL) — [SSD Nodes](https://www.ssdnodes.com/learn/lang/es/tailscale-pricing-explained); [Costbench](https://costbench.com/software/business-vpn/tailscale/free-plan)

**WireGuard propio**
- No hice búsquedas específicas. Inferencia técnica: WireGuard autogestionado entre un VPS en la UE (con IP pública) y el Mac en casa elimina terceros de EE. UU. del camino de datos. A cambio, uno mismo gestiona claves, actualizaciones y la terminación TLS en el VPS.

### Inferences
- RGPD: con Cloudflare (gratis, Pro o Business), un encargado estadounidense ve en claro facturas con datos personales. Hay que incluirlo como subencargado en el DPA con las gestorías y apoyarse en su DPA y en el mecanismo de transferencias (DPF/SCC; no verificado en esta búsqueda). Con Tailscale Funnel o WireGuard, el tercero solo ve tráfico cifrado y metadatos, lo que es más fácil de defender ante un cliente.
- El plan gratuito Personal de Tailscale no es apto para uso comercial. Para un SaaS haría falta un plan de pago, o bien usar Tailscale solo como red interna (Mac ↔ VPS UE) y exponer la web desde el VPS.
- En el patrón D, la mejor práctica es no exponer el Mac en absoluto: solo abre conexiones salientes y no necesita túnel de entrada.

### Gaps
- Página oficial de precios de Tailscale (número de usuarios y dispositivos en 2026) y cifras de ancho de banda de Funnel.
- Estado del DPF UE-EE. UU. en noviembre de 2026 para Cloudflare y Tailscale (no buscado).
- Precio de la DLS de Cloudflare (solo Enterprise, sin precio público).

## 3. Mac alquilado en un CPD de la UE (opción E): Scaleway, AWS EC2 Mac, MacStadium y otros

### Takeaway
La opción UE más barata con certificaciones serias es Scaleway Apple silicon en París: Mac mini M4-S (16 GB/256 GB) a 0,22 €/h o 149 €/mes, y M4-M (32 GB/1 TB) a 0,29 €/h o 199 €/mes, con un mínimo de 24 h por la licencia de Apple. Scaleway tiene ISO 27001:2022 y HDS, aunque el alcance concreto para los Mac está por verificar. AWS EC2 Mac en Irlanda o Frankfurt cuesta unos 1,35-1,48 $/h por host dedicado (aprox. 990-1.080 $/mes) con mínimo de 24 h: entre 5 y 7 veces más caro. Hay proveedores neerlandeses más baratos (Green Mini desde 69 €/mes; vBoxx con M6/M5 Pro desde 140 €/mes sin IVA, con ISO 27001 declarado).

### Cited Findings
**Scaleway (París, FR)**
- Página de precios (vía snippet): M4-S con 16 GB/256 GB a 149 €/mes o 0,22 €/h; M4-M con 32 GB/1,02 TB a 199 €/mes o 0,29 €/h (oficial vía snippet, fecha de captura desconocida) — [Scaleway pricing](https://scaleway.com/en/pricing/apple-silicon)
- Listado de terceros: Scaleway M4-M a 199 €/mes — [WHTop](https://www.whtop.com/plans/scaleway.com/146128)
- Mínimo de 24 h (Green Mini, competidor, citando docs de Scaleway a jun-2026; y cobertura de 2021 del M1) — [Green Mini vs Scaleway](https://www.greenmini.nl/compare/scaleway-alternative/); [Computerworld 2021 (ANTIGUO)](https://www.computerworld.com/article/3605768/how-to-rent-a-virtual-m1-mac-mini-for-12-cents-an-hour.html)
- Docs: el arrendamiento mínimo de Apple silicon es de 24 h. M4, M2 Pro y M2 están en PARIS 1; M1 en PARIS 3 — [Scaleway docs quickstart](https://www.scaleway.com/en/docs/apple-silicon/quickstart/)
- Hay un nivel M4 Pro (llamado "M4-XL" en la página de alta). La nomenclatura es inconsistente — [Scaleway signup](https://www.scaleway.com/en/mac-mini-signup/)
- Certificaciones: ISO/IEC 27001:2022 en datacenters de París (OPCORE PAR1-PAR5) y certificado HDS 809731 (alcance Francia, desde jul-2024) según el directorio de BSI; SecNumCloud en curso (fuente secundaria). No consta qué CPD aloja los Mac — [BSI HDS 809731](https://www.bsigroup.com/en-GB/products-and-services/assessment-and-certification/validation-and-verification/client-directory-certificate/HDS%20809731); [cloudlandscape](https://cloudlandscape.github.io/en/providers/scaleway/)
- En 2021 los Mac M1 estaban en DC4, un antiguo refugio antinuclear a 25 m bajo tierra en París (ANTIGUO) — [Scaleway news 2021](https://www.scaleway.com/en/news/scaleway-introduces-apple-silicon-m1-as-a-service-first-of-its-kind-in-europe/)

**AWS EC2 Mac**
- mac-m4 Dedicated Host bajo demanda: 1,353 $/h en eu-west-1 (Irlanda); 1,476 $/h en eu-central-1 (Frankfurt); 1,23 $/h en us-east-1 (agregadores que citan la AWS Price List API) — [macyou.co](https://macyou.co/blog/aws-ec2-mac-pricing-explained); [computingforgeeks](https://computingforgeeks.com/ec2-mac-instance/)
- Rango mensual de EC2 Mac en 2026: 641-1.438 $/mes según el tipo (agregador) — [macyou.co review](https://macyou.co/reviews/aws-ec2-mac)
- Mínimo de 24 h de asignación y facturación por host dedicado (Bitrise, citando la página de precios de AWS); se factura por host, haya instancias o no; hay Savings Plans — [Bitrise docs](https://docs.bitrise.io/en/bitrise-platform/infrastructure/bitrise-on-aws--manual-setup/allocating-a-dedicated-host-for-mac-instances); [Vantage](https://cur.vantage.sh/aws/amazonec2/dedicated-host/hostusage:mac2-m2/)
- Ejemplo: una sesión de 3 h en mac-m4 cuesta 29,52 $ (24 h × 1,23 $, us-east-1) — [macrun.dev](https://macrun.dev/ec2-mac-alternative)
- Frankfurt mac2 (M1) a 1,298 $/h según un blog personal sin fecha (ANTIGUO o a verificar) — [wilsonmar](https://wilsonmar.github.io/macos-aws)

**MacStadium**
- M4.S (16 GB/256 GB) a 119 $/mes (listados de terceros y competidor). No encontré precio UE — [Green Mini vs MacStadium](https://www.greenmini.nl/compare/macstadium-alternative/)
- Certificaciones declaradas: ISO 27001/27017/27018, SOC 1 y 2 Tipo 2 y prácticas RGPD (blog propio); la página de finanzas cita SOC 1/2/3 — [MacStadium blog](https://macstadium.com/blog/macstadium-experienced-partner-for-mac-clouds); [MacStadium finance](https://macstadium.com/industry/finance)
- No confirmé ubicación de CPD en la UE ni su precio.

**Otros en la UE**
- vBoxx (Países Bajos): ISO 27001 declarado, CPD Tier III NL con "ISO 27001 / NIS2 / GDPR"; M4 Premium a 195 €/mes sin IVA (ficha del 12-may-2026); la línea actual M6/M5 Pro desde 140 €/mes sin IVA con facturación anual — [vBoxx specs PDF](https://mac-hosting.vboxx.eu/downloads/vboxx-mac-mini-hosting-specs.pdf); [vBoxx Mac hosting](https://mac-hosting.vboxx.eu/)
- Green Mini Host (Países Bajos): M4 desde 69 €/mes, tarifa plana sin permanencia (autodeclarado); no encontré certificación ISO — [Green Mini](https://www.greenmini.nl/compare/aws-ec2-mac-alternative/)
- Otros con oferta de Mac mini en Europa (no investigados): Adminor (Estocolmo), Neolo (Alemania), Unihost — [Adminor](https://adminor.net/mac-mini-hosting-en/); [Neolo](https://www.neolo.com/deutschland/mac-mini-hosting/); [Unihost](https://unihost.com/dedicated/mac-mini/)
- OVHcloud: no encontré oferta de Mac en estas búsquedas (a verificar).

### Inferences
- Coste anual 24/7: Scaleway M4-S unos 1.788 €/año (M4-M unos 2.388 €); AWS mac-m4 en Irlanda unos 11.850 $/año (1,353 × 8.760). Un Mac mini propio de unos 1.100-1.300 € sale más barato que un año de Scaleway, pero sin CPD, SLA ni certificaciones.
- Para picos trimestrales (la semana antes del 20 de ene/abr/jul/oct), el mínimo de 24 h permite alquilar Macs extra solo esos días. Por ejemplo, 7 días × 24 h × 0,22 € ≈ 37 € por Mac M4-S y por cierre en Scaleway (cálculo propio). Es una forma razonable de escalar la parte de Apple Vision.
- Scaleway (francés, sujeto a la ley europea, ISO 27001 y HDS) es más fácil de justificar ante una gestoría que AWS (EE. UU., aunque con región UE) o MacStadium (EE. UU.).

### Gaps
- Precios oficiales vigentes de Scaleway y AWS (sitios bloqueados para fetch). No sé si Scaleway ya ofrece Mac mini M5 o M6 ni a qué precio.
- Ancho de banda o transferencia incluidos en Scaleway Apple silicon.
- Ubicación UE y precio de MacStadium; oferta Mac de OVHcloud.
- Qué CPD de Scaleway cubren los certificados ISO 27001 y HDS en el caso de los Mac mini.

## 4. Modelo híbrido (D): worker en casa que solo hace conexiones salientes a una cola en la nube UE

### Takeaway
El patrón recomendable es este: web, cola y almacenamiento cifrado en un cloud de la UE, y el Mac de casa como worker "pull" que solo abre conexiones salientes (HTTPS o túnel WireGuard/Tailscale hacia el VPS), descarga el documento, lo procesa en memoria con Apple Vision, devuelve el resultado y borra. Así se evitan los puertos abiertos, el CG-NAT y la exposición pública del Mac doméstico. Los riesgos principales son la disponibilidad (cortes de luz o fibra en la semana de cierre) y la seguridad física del equipo. Se mitigan con un SAI, backup 4G, cifrado de disco y no persistir datos en casa. Como Apple Vision es solo OCR "de rescate", si el Mac cae la cola se acumula sin perder datos, o se activa un Mac alquilado de Scaleway por 24 h.

### Cited Findings
- Apenas hay fuentes específicas sobre este patrón en esta búsqueda; lo que sigue se apoya en las fuentes de las secciones 1-3.
- El Mac en casa probablemente quede detrás de CG-NAT o IP dinámica (Digi), lo que favorece un worker con conexión solo saliente — [Kompara](https://kompara.es/internet/precio/fibra-mas-barata-espana-hoy); [Bandaancha](https://bandaancha.eu/articulos/tarifas/2)
- Tailscale cifra de extremo a extremo con WireGuard, y DERP solo retransmite tráfico ya cifrado. Sirve como canal privado Mac ↔ VPS UE sin exponer el Mac — [Tailscale encryption](https://tailscale.com/kb/1504/encryption)
- Contratos residenciales que prohíben "servidores" o servicios a terceros. Un worker solo saliente no es un servidor accesible, aunque sigue siendo uso comercial de la línea — [Condiciones cooperativa](https://www.marianoacosta.coop/wp-content/uploads/2019/10/Condiciones-Particulares-y-Generales-WEB.pdf)
- Un Mac alquilado se puede usar como respaldo puntual con mínimo de 24 h (Scaleway 0,22 €/h) — [Scaleway pricing](https://scaleway.com/en/pricing/apple-silicon)

### Inferences
- Diseño sugerido (inferencia técnica):
  1. Cola en el VPS UE (Redis, Postgres con SKIP LOCKED o una cola gestionada), consultada por el worker mediante long-polling HTTPS autenticado con token o mTLS, o a través de Tailscale.
  2. URLs prefirmadas de corta duración para descargar y subir objetos cifrados, con cifrado a nivel de objeto.
  3. Procesamiento en RAM o en directorio temporal, con borrado inmediato. FileVault activado, sin datos persistentes en casa.
  4. Heartbeat y timeouts de lease para reencolar trabajos si el Mac cae.
  5. Credenciales del worker con permisos mínimos (solo leer trabajos asignados y escribir resultados).
- Riesgos de datos en casa: robo o acceso físico (lo mitigan FileVault y no persistir); el domicilio como "ubicación de tratamiento" debe aparecer en el registro de actividades y en el DPA; la seguridad física no es auditable por el cliente.
- Corte de luz en la semana de cierre: un SAI de 650-700 VA (unos 90-115 €) aguanta un Mac mini de pocos vatios bastante tiempo (autonomía no verificada), pero no protege si cae la fibra. El backup 4G/5G (unos 12 €/mes) cubre ese caso. Como el router de fibra o ONT también necesita SAI, hay que dimensionar para el conjunto.
- Degradación elegante: RapidOCR por CPU puede ejecutarse en el cloud UE (Linux), y Apple Vision solo se necesita para los casos de rescate. Si el Mac falla, el SaaS sigue funcionando con menor calidad de OCR en algunos documentos.
- Escalado: con 0-3 tenants basta un Mac en casa; con 10-30 tenants conviene añadir 1-2 Macs alquilados (Scaleway) como workers adicionales del mismo patrón pull, al menos durante las semanas de cierre.

### Gaps
- Autonomía real de un SAI de 650 VA con Mac mini, router y ONT (no buscada).
- Estadísticas de cortes de suministro eléctrico y de fibra en Madrid (no buscadas).

## 5. Confianza que transmite cada opción a una gestoría

### Takeaway
De más a menos confianza: (E) Mac en un CPD de la UE certificado (Scaleway con ISO 27001 y HDS, o vBoxx con ISO 27001) > (D) híbrido con datos y web en un cloud de la UE y un Mac en casa que no almacena nada > (A) todo en un Mac en casa. Para gestorías que tratan datos personales de terceros, lo que se puede enseñar es lo que cuenta: certificaciones del proveedor, DPA y ubicación en la UE. Un servidor doméstico es difícil de justificar en un cuestionario de seguridad del cliente.

### Cited Findings
- Scaleway: ISO 27001:2022 y HDS (BSI); SecNumCloud en curso — [BSI](https://www.bsigroup.com/en-GB/products-and-services/assessment-and-certification/validation-and-verification/client-directory-certificate/HDS%20809731); [cloudlandscape](https://cloudlandscape.github.io/en/providers/scaleway/)
- vBoxx: ISO 27001, NIS2 y RGPD declarados, CPD Tier III NL — [vBoxx specs PDF](https://mac-hosting.vboxx.eu/downloads/vboxx-mac-mini-hosting-specs.pdf)
- MacStadium: ISO 27001/27017/27018, SOC 1/2 Tipo 2 (autodeclarado; empresa de EE. UU.) — [MacStadium blog](https://macstadium.com/blog/macstadium-experienced-partner-for-mac-clouds)
- Cloudflare sin DLS: el TLS termina fuera del control regional; la DLS solo está disponible en Enterprise — [Cloudflare Docs](https://developers.cloudflare.com/data-localization/faq); [donneespersonnelles.fr](https://donneespersonnelles.fr/cloudflare-rgpd)
- Tailscale Funnel: el relay no puede descifrar el contenido — [Tailscale Funnel docs](https://tailscale.com/kb/1223/tailscale-funnel)

### Inferences
- (A) Mac en casa, expuesto con un túnel: confianza baja. Sin certificaciones, con riesgo físico y eléctrico, posible incumplimiento del contrato residencial y, si se usa Cloudflare gratis, un tercero de EE. UU. que ve los datos en claro. Aceptable solo para un piloto con 0-1 tenant, con consentimiento informado.
- (D) Híbrido: confianza media-alta. El "sistema de registro" (web, BD, almacenamiento) vive en un cloud certificado de la UE; el Mac doméstico es un procesador efímero sin datos en reposo. Hay que declararlo en el DPA como ubicación o subencargo y describir las medidas (FileVault, borrado, canal cifrado).
- (E) Mac alquilado en la UE: confianza alta y documentación sencilla (proveedor de la UE, ISO 27001). Cuesta unos 149-199 €/mes por Mac en Scaleway. Lo más razonable es combinarlo con la parte web y de almacenamiento en el mismo proveedor o en otro de la UE.
- Ruta sugerida: empezar con D (Mac propio como worker y cloud de la UE) con 0-3 tenants; a partir de unos 10 tenants, o cuando un cliente pida certificaciones, pasar el worker de Apple Vision a Scaleway (E), manteniendo el Mac de casa como capacidad extra o de respaldo.

### Gaps
- No encontré guías específicas (AEPD o colegios profesionales) sobre servidores domésticos para tratamiento de datos de clientes de gestorías.
