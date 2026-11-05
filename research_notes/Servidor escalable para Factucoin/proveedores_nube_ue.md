# Proveedores cloud UE (VPS/dedicado y PaaS/contenedores) para el SaaS de gestorías (Factucoin), noviembre 2026

Notas de investigación del 5 de noviembre de 2026.

**Método y límites.** WebFetch no estaba disponible: costgoat.com, scaleway.com, hetzner.com y docs.hetzner.com devolvieron ENOTFOUND, porque no están en la lista de dominios permitidos de la sesión. Por eso todas las cifras salen de fragmentos (snippets) de WebSearch. Etiquetas:
- **[OFICIAL]**: el fragmento viene del dominio del propio proveedor.
- **[AGREGADOR]**: blog, comparador o tracker de terceros.
- **"a verificar"**: no se pudo confirmar en la fuente oficial.

Los precios son mensuales en EUR sin IVA salvo que se indique otra cosa. Los cálculos "×730 h" son míos. Los datos que no se encontraron en esta sesión y vienen de conocimiento previo llevan la marca **[conocimiento previo, a verificar]** y nunca se presentan como hechos con fuente.

Para dimensionar uso esta hipótesis de carga, que es inferencia y no un dato:
- **1 tenant:** 2 vCPU / 4 GB.
- **3 tenants:** 4 vCPU / 8 GB.
- **10 tenants:** 8 vCPU / 16 GB, más un worker de OCR aparte en pico.
- **30 tenants:** 16 vCPU o más / 32–64 GB, o bien 2–3 nodos más PostgreSQL gestionado.

El OCR depende de la CPU, así que la vCPU dedicada (o el dedicado bare-metal) importa más en los picos trimestrales (semana anterior al 20 de enero, abril, julio y octubre).

---

## 1. Precios actuales de Hetzner Cloud tras las subidas de abril y junio de 2026, y disponibilidad de CX/CAX

### Takeaway
Hetzner subió precios dos veces en 2026:
- **1 de abril:** alrededor de +30–37 % en toda la gama, incluidos volúmenes, snapshots y Object Storage.
- **15 de junio de 2026 a las 08:00 CEST:** CPX y CCX subieron +113–176 %; CX y CAX, alrededor de +30–38 %. Esta segunda subida se aplica solo a pedidos nuevos y a *rescales*.

Tras junio, CX y CAX siguen siendo baratos (CX23 a 5,49 €, CX33 a 8,49 €, CX43 a 15,99 €, CAX21 a 10,49 €, CAX31 a 20,99 €). En cambio, la vCPU dedicada (CCX) ya no es una ganga (CCX13 a 42,99 €). Hay informes de falta de stock de CX/CAX. Todas las cifras son de agregadores; no se pudo acceder a la página oficial.

### Cited Findings
**Calendario de las subidas**
- Primera subida anunciada el 23 de febrero y efectiva el 1 de abril de 2026, de alrededor de un tercio en servidores cloud. La segunda entró en vigor el 15 de junio de 2026 a las 08:00 CEST — [AGREGADOR] [northflank](https://northflank.com/blog/hetzner-cloud-server-price-increases); [AGREGADOR] [wz-it](https://wz-it.com/en/blog/hetzner-price-increase-june-2026-cpx-ccx-alternatives/)
- Prensa técnica sobre la subida de abril: "hasta un 37 %" — [Tom's Hardware](https://www.tomshardware.com/tech-industry/hetzner-to-raise-prices-by-up-to-37-percent-from-april-1); [heise](https://heise.de/-11185981). Sobre la de junio: "hasta un 200 %" — [heise](https://heise.de/-11333037)
- Otro cronograma cuenta cuatro acciones de precio en 2026: tarifas de alta (setup) en febrero, la subida general del 30–37 % el 1 de abril, tarifas de alta de dedicados el 29 de abril y la subida de junio — [AGREGADOR] [webhosting.today, 29-05-2026](https://webhosting.today/2026/05/29/hetzner-has-now-raised-prices-three-times-in-2026-this-one-is-different/). Hetzner tiene un comunicado oficial sobre las tarifas de alta: [OFICIAL] [hetzner.com pressroom](https://www.hetzner.com/pressroom/statement-on the-latest-adjustment-to setup-fees/), con contenido no leído.
- Hetzner mantiene una página oficial de ajustes de precio, con tablas no leídas porque el fetch estaba bloqueado: [OFICIAL] [docs.hetzner.com price-adjustment](https://docs.hetzner.com/de/general/infrastructure-and-availability/price-adjustment/)
- La subida de junio se aplica a pedidos nuevos y a rescales, no a servidores existentes que no se redimensionen — [AGREGADOR] [rscomputers-ks](https://rscomputers-ks.com/hetzner-price-increase-2026-move-servers/); [AGREGADOR] [agentdeals](https://agentdeals.dev/hetzner-pricing-2026)

**CCX (vCPU dedicada, DE/FI), precio anterior → precio tras junio de 2026**
- CCX13: 15,99 € → 42,99 € (+169 %)
- CCX23: 31,49 € → 85,99 € (+173 %)
- CCX33: 62,49 € → 138,49 € (+122 %)
- CCX53: 249,99 € → 533,49 € (+113 %)

Fuentes: [AGREGADOR] [northflank](https://northflank.com/blog/hetzner-cloud-server-price-increases); [AGREGADOR] [webhosting.today, 18-06-2026](https://webhosting.today/2026/06/18/hetzners-price-increases-reached-209-the-30-headline-applied-to-a-different-tier/); [AGREGADOR] [byteiota](https://byteiota.com/hetzner-june-2026-price-shock/)

**CPX (AMD compartido)**
- CPX22: 7,99 € → 19,49 €. En la UE las subidas de CPX fueron de alrededor de +144–175 %, y en EE. UU. superaron el +200 % — [AGREGADOR] [northflank](https://northflank.com/blog/hetzner-cloud-server-price-increases); [AGREGADOR] [privatedevops](https://privatedevops.com/news/hetzner-june-2026-cloud-price-increase-what-to-do)

**CX (Intel/AMD compartido, "cost-optimized") y CAX (Arm Ampere)**

| Plan | Especificación | Precio | Fuente |
|---|---|---|---|
| CX23 | 2 vCPU / 4 GB / 40 GB [conocimiento previo, a verificar] | 2,99 € antes de abril → 3,99 € en abril → 5,49 € tras junio | [pricetimeline](https://pricetimeline.com/news/211) para abril; [stackvaluelab](https://stackvaluelab.com/hetzner-price-increase-2026/) para junio |
| CX33 | 4 vCPU / 8 GB | 6,49 € → 8,49 € tras junio | [cloudtally](https://cloudtally.eu/hetzner-cloud-prices); [bitdoze](https://www.bitdoze.com/hetzner-cloud-review/) |
| CX43 | 8 vCPU / 16 GB | 11,99 € → 15,99 € | [bitdoze](https://www.bitdoze.com/hetzner-cloud-review/) |
| CAX11 | — | 3,29 € → 4,49 € en abril → 5,99 € tras junio | [pricetimeline](https://pricetimeline.com/news/211); [stackvaluelab](https://stackvaluelab.com/hetzner-price-increase-2026/) |
| CAX21 | 4 vCPU Arm / 8 GB | 7,99 € → 10,49 € | [eucloudcost](https://www.eucloudcost.com/providers/hetzner/) |
| CAX31 | 8 vCPU Arm / 16 GB | 15,99 € → 20,99 € | [eucloudcost](https://www.eucloudcost.com/providers/hetzner/) |

Todas las fuentes de la tabla son [AGREGADOR].

- Un comparador titula "VPS from €5.49/mo, 20 TB Free Egress" — [AGREGADOR] [eucloudcost](https://www.eucloudcost.com/providers/hetzner/)
- Discrepancia: un blog sitúa el CX23 en alrededor de 5,83 € antes de abril, lo que no cuadra con los 2,99 € de otras fuentes. Probablemente es un error o usa otra base — [AGREGADOR] (síntesis de búsqueda; [stackvaluelab](https://stackvaluelab.com/hetzner-price-increase-2026/), [bex.co](https://bex.co/blog/2026/08/16/hetzner-double-price-hike-cheap-box-assumption-cost-model))

**Disponibilidad de CX/CAX**
- Hay un artículo titulado "Hetzner CX and CAX Unavailable: What to Buy Instead (2026)", que indica problemas de stock en algún momento de 2026. No se pudo confirmar si persisten en noviembre — [AGREGADOR] [stackvaluelab](https://stackvaluelab.com/hetzner-cx-cax-unavailable/)
- Las fuentes recomiendan pasar las cargas de CPX/CCX a CAX como alternativa barata — [AGREGADOR] [northflank](https://northflank.com/blog/hetzner-cloud-server-price-increases)

**Extras**
- **IPv4 primaria:** 0,50 €/mes. Algunas webs dan precios "con IPv4" (8,99 €, 16,49 €, 10,99 €, 21,49 €), es decir, el precio de lista más 0,50 € — [AGREGADOR] [bitdoze cost-optimized](https://www.bitdoze.com/hetzner-cloud-cost-optimized-plans/). A verificar en la web oficial.
- **Tráfico incluido:** 20 TB/mes en los planes de la UE — [AGREGADOR] [bestusavps](https://bestusavps.com/reviews/hetzner/); [eucloudcost](https://www.eucloudcost.com/providers/hetzner/). No se encontró el precio por TB de exceso.
- **Volúmenes:** 0,0440 → 0,0572 €/GB/mes desde abril (alrededor de 5,72 €/100 GB) — [AGREGADOR] [docs.elest.io aviso abril](https://docs.elest.io/books/announcement/page/hetzner-price-change-notice-effective-april-1st); [bitdoze ES](https://www.bitdoze.com/md/es/hetzner-cloud-precios-2026.md); [cloudpricecheck](https://cloudpricecheck-com.pages.dev/hetzner/hetzner-volumes-pricing)
- **Snapshots:** 0,0110 → 0,0143 €/GB/mes — mismas fuentes [AGREGADOR].
- **Object Storage:** el precio base sube de 4,99 € a 6,49 € al mes. Según el fragmento, ese precio base incluye 1 TB; esto queda a verificar — [AGREGADOR] [agentdeals](https://agentdeals.dev/hetzner-pricing-2026); [findstack](https://findstack.com/resources/hetzner-price-increase-2026)
- **Backups automáticos:** no se encontró fuente para 2026. Históricamente costaban el 20 % del precio del servidor [conocimiento previo, a verificar].

**Dedicados (AX)**
- Las cifras del AX42 son contradictorias:
  - Una tabla de junio de 2026 da 187,30 €/mes y 94,00 € de alta (FSN/HEL, sin IPv4). Parece muy alta y puede que no sea un AX42 estándar — [AGREGADOR] [prismix.dev](https://prismix.dev/news/e099eaeb0874)
  - Una página antigua en alemán da 115,79 €.
  - En abril se informó de una subida de 56,29 € a 68,19 €/mes — [deskmodder](https://www.deskmodder.de/blog/?p=213645); [heise](https://heise.de/-11185981)
  - En LowEndTalk se cita una subida de la tarifa de alta del AX42 de 79 € a 107 € — [lowendtalk](https://lowendtalk.com/discussion/214154/hetzner-increases-setup-fees-order-on-spacecore-at-the-old-price-while-you-can)
  - Conclusión: el precio actual del AX42/AX52 queda a verificar.
- Motivo oficial que se cita: "exceptionally high purchase prices for hardware components" (DRAM/SSD) — [datacenterdynamics](https://www.datacenterdynamics.com/en/news/german-cloud-firm-hetzner-hikes-prices-by-up-to-50-percent-due-to-drastic-component-price-increases); [lavx](https://news.lavx.hu/article/hetzner-implements-up-to-37-price-hike-across-cloud-services-amid-dram-supply-crunch)

### Inferences
- **Dimensionado en Hetzner con CX tras junio, a 0,50 € por IPv4:**

  | Tenants | Configuración | Coste aproximado |
  |---|---|---|
  | 1 | CX23 + volumen de 50 GB | 5,49 + 0,50 + 2,86 ≈ 8,9 €/mes |
  | 3 | CX33 | ≈ 9 € |
  | 10 | CX43 (16 GB) + worker de OCR CX33 o CAX21 temporal en pico | ≈ 16,5 + 9–11 € |
  | 30 | CCX33 (138,49 €) o varios CX43 más PostgreSQL autogestionado | — |

  Para 30 tenants, comparar con un dedicado AX, cuyo precio está a verificar.
- **El rescale ahora tiene coste.** Como la subida de junio se aplica a rescales, redimensionar un servidor antiguo lo pasa a la tarifa nueva. Conviene diseñar con escalado horizontal (servidores nuevos detrás de un balanceador) en vez de subir plan "en caliente".
- **CAX (Arm) es atractivo, pero hay que comprobar rendimiento y ruedas.** onnxruntime tiene builds aarch64 [conocimiento previo, a verificar], pero hay que medir el rendimiento de RapidOCR en Ampere frente a x86 antes de elegir.
- **Para OCR en pico, CX compartido es arriesgado** (vecinos ruidosos). Al menos el worker de OCR debería ir en CCX o dedicado en 10–30 tenants, o bien en servidores CX efímeros que se crean y destruyen cada trimestre, facturados por hora [conocimiento previo, a verificar].
- **Datos generales de Hetzner [conocimiento previo, a verificar]:** empresa alemana (Gunzenhausen) sin matriz estadounidense, sin exposición directa a la CLOUD Act. Centros UE en Falkenstein, Núremberg y Helsinki; sin región en España. ISO 27001 en sus centros. DPA (AVV) firmable en la consola. Sin PostgreSQL gestionado propio.

### Gaps
- No se pudo leer hetzner.com ni docs.hetzner.com (dominios bloqueados). Todas las cifras de Hetzner son de agregadores y quedan a verificar en la [tabla oficial](https://docs.hetzner.com/de/general/infrastructure-and-availability/price-adjustment/).
- Falta el precio de CX53, CAX41, backups y Load Balancer tras junio.
- No se sabe si en noviembre de 2026 hay stock de CX/CAX en FSN/NBG/HEL.
- Precio actual de dedicados AX42/AX52/AX102 tras junio: cifras contradictorias.

---

## 2. Otros proveedores UE: planes, almacenamiento, bases de datos gestionadas, ubicaciones, certificaciones, CLOUD Act y facilidad de escalado

### Takeaway
- **OVHcloud:** tiene página de VPS para España y la cuota de mercado más amplia. Sus VPS 2026 son baratos (VPS-1 alrededor de 6,49 €, VPS-3 alrededor de 10,40 €, según agregadores), el tráfico es ilimitado o generoso, tiene ENS de nivel alto (según un listado de terceros) y SecNumCloud en IaaS. Su PostgreSQL gestionado es caro para empezar (alrededor de 64 USD al mes).
- **Scaleway:** facturación por hora, PostgreSQL gestionado y Serverless Containers por segundo. Tiene ISO 27001 y HDS; SecNumCloud está en evaluación. Precios de instancias más altos que Hetzner CX.
- **IONOS:** tiene centro en Logroño (España), pero sus precios de entrada son promocionales y no se encontró ENS.
- **UpCloud / Infomaniak:** datos escasos; no se encontró región en Madrid.

### Cited Findings
**OVHcloud (Francia)**
- **VPS en España:** la página oficial muestra VPS-1 desde 4,54 USD/mes (2 vCore, 4 GB, 40 GB NVMe) hasta VPS-4 desde 23,37 USD/mes (8 vCore, 24 GB). Está en USD y no indica el centro de datos — [OFICIAL] [ovhcloud.com/en/vps/vps-espana](https://www.ovhcloud.com/en/vps/vps-espana/)
- **Precios VPS en EUR según agregadores:**
  - VPS-1 2026 a 6,49 €/mes y VPS-2 2026 a 9,99 €/mes, según la API de OVH, verificado el 1-10-2026 — [AGREGADOR] [vpsledger](https://vpsledger.com/providers/ovhcloud/)
  - VPS-3 a 10,40 €/mes, verificado el 25-10-2026 — [AGREGADOR] [trackvps](https://trackvps.com/plans/ovh-vps-3)
  - Las fuentes no coinciden entre sí: a verificar.
- **VPS-2 en Local Zones:** se ofrece en Local Zones de 28 ciudades. No se confirmó Madrid — [OFICIAL] (fragmento de la [página VPS España](https://www.ovhcloud.com/en/vps/vps-espana/))
- **PostgreSQL gestionado (precios por nodo en USD, posiblemente antiguos):**
  - Discovery: desde 64,24 USD/mes (1 nodo, backups de 48 h, sin SLA).
  - Production: desde 81,76 USD/mes (2 nodos, multi-AZ, backups de 14 días, SLA del 99,95 %).
  - Advanced: desde 83,07 USD/mes (3 nodos).
  
  Fuente: [OFICIAL] [ovhcloud.com/en/public-cloud/postgresql](https://www.ovhcloud.com/en/public-cloud/postgresql/). Un comparador da 63,36 USD/mes por un Discovery de 2 vCPU / 4 GB / 80 GB — [AGREGADOR] [getdeploying](https://getdeploying.com/ovh)
- **Certificaciones:**
  - ENS (España) de nivel Alto según un directorio de terceros, a verificar en la página de compliance de OVH — [AGREGADOR] [cloudlandscape](https://cloudlandscape.github.io/en/providers/ovhcloud/)
  - SecNumCloud en IaaS; OVH MKS y Scaleway Kapsule quedan fuera de SecNumCloud (octubre de 2026) — [AGREGADOR] [qovery](https://www.qovery.com/blog/numspot-ovhcloud-scaleway-secnumcloud-sovereign-cloud-comparison)
- **Managed Kubernetes:** OVH lanzó en enero de 2026 un tier MKS "Standard" desplegado en regiones 3-AZ. No se confirmó si el plano de control es gratuito en ese tier — [AGREGADOR] (síntesis de búsqueda; [invgate](https://invgate.com/itdb/ovhcloud-managed-kubernetes))
- **Contexto corporativo:** OVH empuja su oferta de cloud soberano y reorganizó ventas en 2026 — [AGREGADOR] [webhosting.today, 02-06-2026](https://webhosting.today/2026/06/02/ovhcloud-restructures-sales-for-a-sovereign-cloud-market-that-just-got-real/); [domain-b](https://www.domain-b.com/technology/technology-general/ovhcloud-sovereign-cloud-h1-2026-results)

**Scaleway (Francia, grupo Iliad)**
- **Instancias:**
  - DEV1-S (2 vCPU / 2 GB): 0,0088 €/h, que pasa a 0,00898 €/h desde el 1-6-2026, unos 6,56 €/mes según mi cálculo ×730 — [OFICIAL] [blog Scaleway "transparent update on pricing"](https://www.scaleway.com/en/blog/a-transparent-update-on-scaleway-pricing/). Un comparador da "VMs from €6.55/mo" — [AGREGADOR] [eucloudcost](https://www.eucloudcost.com/providers/scaleway/)
  - POP2-4C-16G (4 vCPU dedicadas / 16 GB): 0,147 €/h, unos 107 €/mes — [OFICIAL] [tarifas virtual instances (FR)](https://www.scaleway.com/fr/tarifs/virtual-instances/)
  - PLAY2-PICO (1 vCPU / 2 GB) a unos 11,51 USD/mes y PLAY2-MICRO (4 vCPU / 8 GB) a unos 44,39 USD/mes — [AGREGADOR] [getdeploying](https://getdeploying.com/aws-vs-scaleway)
- **Block Storage:**
  - 0,000118 → 0,00013 €/GB/h desde el 1-6-2026, unos 0,095 €/GB/mes — [OFICIAL] [blog de precios](https://www.scaleway.com/en/blog/a-transparent-update-on-scaleway-pricing/)
  - En la página de bases de datos: Block 5K a 0,0993 €/GB/mes y Block 15K a 0,1489 €/GB/mes — [OFICIAL] [managed-databases pricing](https://www.scaleway.com/en/pricing/managed-databases-pricing/)
- **PostgreSQL gestionado:** existe DB-DEV-S (2 vCPU / 2 GB). El precio por hora no se pudo leer sin ambigüedad: a verificar. Backups y snapshots a 0,03 €/GB/mes — [OFICIAL] [managed-databases pricing](https://www.scaleway.com/en/pricing/managed-databases-pricing/)
- **Object Storage:** las fuentes se contradicen. Una da unos 19,69 USD por 1 TB más 250 GB de egress (alrededor de 0,02 USD/GB) — [AGREGADOR] [getdeploying](https://getdeploying.com/aws-vs-scaleway). Otra da 0,43 €/GB, que parece un error — [AGREGADOR] [cloudpricecalculators](https://cloudpricecalculators.com/scaleway-calculator/). A verificar.
- **Certificaciones:**
  - ISO 27001:2022. El certificado de BSI cubre París, Lille y otros sitios franceses — [OFICIAL] [security-and-compliance](https://www.scaleway.com/en/security-and-compliance/); [BSI directory](https://www.bsigroup.com/en-GB/products-and-services/assessment-and-certification/validation-and-verification/client-directory-profile/ON_LIN-0047624081-025)
  - HDS desde julio de 2024 (vigente de 2024-06-28 a 2027-06-27) — [OFICIAL] [noticia HDS](https://www.scaleway.com/fr/news/scaleway-annonce-sa-certification-hds-pour-garantir-la-securite-des-donnees-de-sante/)
  - Una entrada de BSI ligada a ISO 27001 muestra caducidad el 2026-12-05 (ambiguo, a verificar).
  - SecNumCloud "en evaluación" — [OFICIAL] [security-and-compliance](https://www.scaleway.com/en/security-and-compliance/)
  - No se encontró ENS ni región en Madrid.

**IONOS (Alemania, United Internet)**
- **Centros de datos:** Frankfurt, Berlín, París, Londres y Logroño (España); 8 centros en Europa y Norteamérica — [AGREGADOR] (síntesis; [bitcatcha](https://www.bitcatcha.com/web-hosting/ionos-review/), [vpslocate](https://vpslocate.com/providers/ionos.html))
- **Cloud VPS (página .com en USD):**
  - Precio promocional de unos 2–20 USD/mes con permanencia de 3 meses o 1 año; lista de 6 USD (VPS S+) a 68 USD (VPS XXL+) — [OFICIAL] [ionos.com/servers/cloud-vps](https://www.ionos.com/servers/cloud-vps)
  - VPS S+ a 6 USD, M+ a 14 USD y L+ a 25 USD, sin promoción — [AGREGADOR] [vpsbenchmarks](https://www.vpsbenchmarks.com/compare/ionos)
  - Aviso: el precio promocional puede doblarse o triplicarse al renovar — [AGREGADOR] [comparevps](https://www.comparevps.com/hosting/ionos)
- **ENS:** no se encontró ninguna fuente sobre ENS de IONOS.

**UpCloud (Finlandia) e Infomaniak (Suiza)**
- **UpCloud:**
  - PostgreSQL/MySQL gestionado de 1 a 3 nodos, hasta 500 GB — [OFICIAL] [upcloud.com/pricing](https://upcloud.com/pricing)
  - "Precios idénticos en sus 15 centros" — [AGREGADOR] [G2](https://www.g2.com/products/upcloud/reviews)
  - Plantilla de precios de terceros: "Fixed prices with zero-cost egress" — [AGREGADOR] [repo extracto](https://repo.jesusperez.pro/jesus/prvng_extensions/raw/branch/main/providers/upcloud/pricing.html)
- **Infomaniak:**
  - Managed Cloud Server a unos 29 €/mes con 50 GB SSD — [AGREGADOR] [infoswitch](https://infoswitch.fr/en/blog/infomaniak-pricing-2026-all-services)
  - Centros solo en Suiza — [AGREGADOR] [vpsbenchmarks](https://www.vpsbenchmarks.com/hosters/infomaniak)
  - Suiza es país con decisión de adecuación de la UE [conocimiento previo, a verificar].

### Inferences
- **Hetzner y PostgreSQL:** ningún proveedor de los mirados ofrece PostgreSQL gestionado barato en Hetzner (no tiene). En OVH cuesta unos 64 USD o más; en Scaleway, DB-DEV-S está probablemente en el rango de 10–20 €/mes [no confirmado, a verificar]. Con 30 tenants, PostgreSQL gestionado (OVH Production o Scaleway con HA) añadiría seguramente de 80 a 150 €/mes.
- **España / ENS:** si los clientes (gestorías) o sus clientes públicos exigen ENS, OVH es el candidato mejor documentado (ENS Alto según un tercero). IONOS (Logroño) es el único con centro en España confirmado en esta búsqueda, pero sin ENS confirmado. El ENS solo es obligatorio para el sector público y sus proveedores [conocimiento previo, a verificar].
- **CLOUD Act [conocimiento previo, a verificar]:** ninguno de estos proveedores tiene matriz estadounidense.
  - Hetzner: Alemania.
  - OVH: Francia. Tiene filial en EE. UU. (OVH US LLC) separada.
  - Scaleway: Iliad, Francia.
  - IONOS: United Internet, Alemania. Tiene filial en EE. UU. para el mercado americano.
  - UpCloud: Finlandia.
  - Infomaniak: Suiza.
  - Clever Cloud: Francia.

  No se encontró fuente directa en esta sesión.
- **Facilidad de escalado [conocimiento previo, a verificar]:**
  - Hetzner: rescale en el panel, volúmenes de hasta 10 TB, salto a dedicado vía vSwitch/Robot. Ahora el rescale aplica precio nuevo.
  - OVH: los VPS se pueden ampliar a un plan superior pero no reducir. El paso a Public Cloud o Bare Metal implica migración.
  - Scaleway: cambio de tipo de instancia apagándola, y Kapsule/Serverless sin migrar código si se conteneriza desde el día 1.

### Gaps
- Precios oficiales en EUR de OVH VPS 2026 y de OVH Object Storage, Block Storage y backups.
- ¿Tiene OVH zona local o región en Madrid?
- Precio de Scaleway Object Storage y DB-DEV-S. ¿Tiene Scaleway región en Madrid (no se encontró)?
- Planes concretos de IONOS en EUR y certificación ENS.
- Planes de UpCloud en EUR. Por limitación de llamadas no se investigaron Clever Cloud ENS, IONOS DBaaS ni OVH MKS en detalle.
- DPA: no se buscó la disponibilidad de DPA por proveedor. Todos los grandes de la UE lo ofrecen [conocimiento previo, a verificar].

---

## 3. Coste de PaaS/contenedores gestionados en la UE a esta escala, y si simplifican la seguridad

### Takeaway
- **Scaleway Serverless Containers:** factura por segundo, a 0,00001 €/vCPU-s y 0,000002 €/GB-s, con un free tier de 200 000 vCPU-s al mes. Un contenedor de 1 vCPU / 2 GB siempre encendido cuesta unos 36 €/mes antes del free tier, varias veces más que un CX33 de Hetzner. Encaja en un modelo híbrido: la web/API en un VPS barato y el OCR como jobs o contenedores que escalan solo en la semana del 20.
- **Clever Cloud:** PaaS francés que soporta Python y Docker, con add-on PostgreSQL con backup diario y 7 días de retención. Precio de entrada de unos 4,80–5,60 €/mes según agregadores, no confirmado.
- **OVH MKS:** existe un tier Standard 3-AZ desde enero de 2026.

El PaaS reduce la superficie de mantenimiento (parches de SO, TLS, backups de base de datos), pero no sustituye a la seguridad de la aplicación ni al aislamiento entre tenants.

### Cited Findings
- **Scaleway Serverless Containers:** 0,00001 €/vCPU-s (1,00 € por 100 000 vCPU-s) tras un free tier de 200 000 vCPU-s por cuenta y mes. Memoria a 0,000002 €/GB-s tras su propio free tier — [OFICIAL] [scaleway.com/en/pricing/serverless](https://www.scaleway.com/en/pricing/serverless/) (vía fragmento)
- **Comparativa de precios de contenedores serverless en 2026** — [AGREGADOR] [danubedata](https://danubedata.ro/blog/serverless-container-pricing-comparison-2026)
- **Clever Cloud:**
  - Entrada de unos 5,60 €/mes — [AGREGADOR] [capterra](https://www.capterra.com/p/173415/Clever-cloud/)
  - "Desde unos 4,80 €/mes la instancia más pequeña" — [AGREGADOR] [itechguides](https://www.itechguides.com/products/clever-cloud/)
  - "Desde 1,49 €/mes", no verificable — [AGREGADOR] (síntesis; [europeanstack](https://europeanstack.com/software/clever-cloud))
- **Clever Cloud PostgreSQL:** el plan DEV es gratuito, pero solo para pruebas (sin backups, extensiones ni SLA). Los planes de pago tienen backup diario gratuito con retención de 7 días — [OFICIAL] [clever-cloud.com/doc/.../postgresql](https://www.clever-cloud.com/doc/deploy/addon/postgresql/)
- **Clever Cloud, lenguajes y escalado:** soporta Python y Docker, y escala en vertical y en horizontal ("scalers"). No se encontró precio por scaler — [AGREGADOR] [thectoclub](https://thectoclub.com/tools/clever-cloud-review/)
- **OVH MKS:** tier Standard 3-AZ (enero de 2026), fuera de SecNumCloud — [AGREGADOR] [qovery](https://www.qovery.com/blog/numspot-ovhcloud-scaleway-secnumcloud-sovereign-cloud-comparison). Scaleway "free control plane" (Kapsule) — [AGREGADOR] [eucloudcost Scaleway](https://www.eucloudcost.com/providers/scaleway/) (titular "Free Control Plane").
- **PaaS frente a Hetzner:** un análisis concluye que, incluso tras la subida del 37 %, una flota de 3 nodos en Hetzner sale más barata que Render o Railway — [AGREGADOR] [bex.co](https://bex.co/blog/2026/08/22/hetzner-april-price-hike-vs-render-railway-three-node-fleet)

### Inferences
- **Cálculos propios con precios oficiales de Scaleway Serverless (730 h/mes):**
  - 1 vCPU continua: 0,036 €/h, unos 26,3 €/mes.
  - 1 GB continuo: 0,0072 €/h, unos 5,3 €/mes.
  - El free tier de 200 000 vCPU-s equivale a unas 55,6 vCPU-hora al mes.
  - Escenario de OCR en pico: un trimestre con 8 vCPU × 40 h de procesamiento = 320 vCPU-h = 1 152 000 vCPU-s, unos 11,5 € por vCPU (o unos 9,5 € tras el free tier), más la memoria. El OCR estacional en serverless es muy barato.
  - El servicio web siempre encendido sale caro en serverless frente a una VM.
- **Ruta de crecimiento recomendable (inferencia):**
  1. **0–3 tenants:** Hetzner CX23/CX33 con IPv4 (unos 6–9 €), backups y volumen, o un VPS de OVH en la UE (unos 6,5–10 €).
  2. **10 tenants:** la aplicación en una VM y el OCR como cola con workers efímeros (más VMs por hora en Hetzner, o Scaleway Serverless Jobs/Containers).
  3. **30 tenants:** PostgreSQL gestionado (Scaleway u OVH) más 2 VMs detrás de un balanceador, o Kubernetes gestionado (Kapsule u OVH MKS).
  
  Contenerizar desde el día 1 (Docker) evita migraciones dolorosas entre estas opciones.
- **Seguridad:**
  - El PaaS o la base de datos gestionada simplifican los parches, el cifrado en reposo, los backups y el TLS.
  - El RGPD sigue exigiendo DPA, registro de actividades, cifrado, control de acceso y aislamiento por tenant (SQLite por fichero con cifrado y permisos, o esquemas/bases de datos separados en PostgreSQL).
  - Hetzner no ofrece nada gestionado salvo Object Storage, Load Balancer y firewall, así que exige más operación propia [conocimiento previo, a verificar].
- **Mejor relación precio/ruta de crecimiento (inferencia):**
  - Hetzner CX/CAX para el arranque y la carga base, si hay stock y aceptando que el rescale aplica precio nuevo.
  - Scaleway como opción "todo en uno" (VM + PostgreSQL gestionado + Serverless + Object Storage, en un mismo proveedor francés) cuando se llegue a 10–30 tenants.
  - OVH si ENS o soberanía pesan en la venta a gestorías.

### Gaps
- Precio oficial actual de Clever Cloud (tamaños XS/S/M, add-on PostgreSQL de pago) y de Scaleway Serverless Jobs / Serverless SQL Database: no confirmados.
- Precio del plano de control y de los nodos de OVH MKS en 2026.
- Benchmarks de RapidOCR/onnxruntime en vCPU compartida frente a dedicada, x86 frente a Arm: no buscados.
- Es necesario permitir en la configuración de red de la sesión los dominios hetzner.com, docs.hetzner.com, scaleway.com y costgoat.com para verificar las cifras en las fuentes oficiales.
