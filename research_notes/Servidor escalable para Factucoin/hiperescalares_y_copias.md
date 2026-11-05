# Hiperescalares en regiones UE/España y copias de seguridad cifradas off-site (Factucoin, noviembre 2026)

Notas de investigación, 2026-11-05. **Limitación del método:** WebFetch estaba bloqueado (DNS ENOTFOUND) para hetzner.com, backblaze.com, aws.amazon.com y scaleway.com, así que no se pudo abrir ninguna página oficial de precios. Todas las cifras salen de fragmentos de WebSearch. Cuando el fragmento procede de una página oficial se marca **[oficial]**; si viene de un agregador o blog, **[agregador]**. Fecha de consulta de todo: 2026-11-05, salvo que se indique otra fecha de la fuente. Las cifras sin confirmar llevan **"a verificar"**. Los precios de AWS/Azure/GCP son en USD, sin IVA y bajo demanda. Los de Hetzner/OVH/Scaleway son en EUR y sin IVA, salvo indicación.

## Pregunta 1: ¿Tiene sentido un hiperescalar con 0-3 clientes frente a un VPS europeo, y cuándo empieza a tenerlo? (coste mensual a 1/3/10/30 clientes, créditos, certificaciones, CLOUD Act, nube soberana)

### Takeaway
Con 1-3 clientes, una configuración mínima en AWS (VM pequeña, RDS micro, IPv4, S3, sin NAT ni balanceador) cuesta unos 45-60 USD/mes más almacenamiento y extras. El equivalente en Hetzner (CX33 + IPv4 + Storage Box) ronda los 13 EUR/mes, incluso después de las subidas de Hetzner de 2026. El hiperescalar no compensa por coste en esa fase, salvo que haya créditos de startup o que algún cliente exija contractualmente ENS Alto, una región en España o un proveedor concreto. Los tres hiperescalares declaran ENS Alto. El CLOUD Act sigue aplicando a sus regiones UE normales, y la AWS European Sovereign Cloud (GA en enero de 2026, en Brandenburgo) es la respuesta más clara a eso, aunque con menos servicios.

### Cited Findings

**Cómputo (VM pequeña)**
- AWS EC2 t4g.medium (2 vCPU ARM / 4 GB) en eu-south-2 (España): unos 0,0368-0,037 USD/h bajo demanda, es decir ~27 USD/mes (×730 h). La reserva a 1 año sale a ~0,014 USD/h. Las fuentes no fechan el precio; a verificar. — [aws-pricing.com](https://aws-pricing.com/t4g.medium.html) [agregador]; [devzero.io eu-south-2](https://www.devzero.io/instances/aws/regions/eu-south-2) [agregador]
- GCP e2-medium en europe-southwest1 (Madrid): la fila del agregador muestra 28,86 como valor mensual aparente (también 0,0395/h y 12,99, que parece spot). Las columnas no tienen etiqueta; a verificar. — [cloudprice.net europe-southwest1](https://cloudprice.net/gcp/regions/europe-southwest1) [agregador]
- Azure Standard_B2s en Spain Central: no hay cifra confirmada. Como referencia, unos 30,37 USD/mes en eastus y 21,90 USD/mes en Germany Central. — [holori](https://calculator.holori.com/azure/vm/standard-b2s) [agregador]; [azurespeed Spain Central](https://www.azurespeed.com/AzureVmPricing/Regions/spaincentral) [agregador]
- Hetzner Cloud subió precios dos veces en 2026: entre un 30 y un 37 % el 1 de abril, y otra vez el 15 de junio de 2026. La subida de junio afecta a pedidos nuevos y a reescalados; las instancias existentes mantienen su precio. — [findstack](https://findstack.com/resources/hetzner-price-increase-2026) [agregador]; [heise](https://heise.de/-11333037); [tomshardware](https://www.tomshardware.com/tech-industry/hetzner-to-raise-prices-by-up-to-37-percent-from-april-1)
- Hetzner CX33 (4 vCPU compartida / 8 GB) tras junio de 2026: probablemente 8,99 EUR/mes sin IVA ni IPv4. Hay una fuente que dice 8,49, así que hay contradicción. La línea CPX sube mucho: CPX22 pasa de 7,99 a 19,49 EUR (+144-175 %). — [bitdoze ES](https://www.bitdoze.com/es/hetzner-cloud-precios-2026/); [wz-it](https://wz-it.com/en/blog/hetzner-price-increase-june-2026-cpx-ccx-alternatives/); [privatedevops](https://privatedevops.com/news/hetzner-june-2026-cloud-price-increase-what-to-do) [agregadores]
- IPv4 primaria en Hetzner: 0,50 EUR/mes, sin cambios en 2026. — mismas fuentes

**BD gestionada**
- RDS PostgreSQL db.t4g.micro (2 vCPU, 1 GB) Single-AZ en Frankfurt: 0,019 USD/h, unos 14 USD/mes. Multi-AZ: 0,037 USD/h, unos 27 USD/mes. No incluye almacenamiento ni backups. Bytebase lo actualizó el 20/07/2026. — [bytebase](https://www.bytebase.com/dbcost/rds/instance/db.t4g.micro/) [agregador]; [sparecores](https://sparecores.com/database/aws/db.t4g.micro) [agregador]
- Azure Database for PostgreSQL Flexible B2s: unos 29 USD/mes (región no confirmada). — [bytebase B2s](https://www.bytebase.com/dbcost/azure-flexible/instance/B2s/) [agregador]
- Precio de Cloud SQL en Madrid: no encontrado (ver Gaps).

**Red y costes ocultos de AWS**
- IPv4 pública: 0,005 USD/IP/h (~3,65 USD/mes) desde el 1/2/2024, esté asociada o no. — [AWS News Blog](https://aws.amazon.com/blogs/aws/new-aws-public-ipv4-address-charge-public-ip-insights) [oficial]
- NAT Gateway: unos 0,045 USD/h (~32,85 USD/mes) más 0,045 USD/GB procesado, más la IPv4. Se multiplica por cada AZ. Esa cifra es de us-east; otra fuente habla de 0,05 USD/h. A verificar para eu-south-2. — [cloudburn](https://cloudburn.io/blog/aws-nat-gateway-pricing) [agregador]
- Salida a Internet: 100 GB/mes gratis (agregado entre servicios y regiones; perpetuo desde el 1/12/2021). Después, unos 0,09 USD/GB para los primeros 10 TB en regiones UE. — [AWS News Blog](https://aws.amazon.com/blogs/aws/aws-free-tier-data-transfer-expansion-100-gb-from-regions-and-1-tb-from-amazon-cloudfront-per-month) [oficial, 2021]; [cloudforecast](https://www.cloudforecast.io/guides/aws-data-transfer-cost/) [agregador]
- S3 Standard: 0,023 USD/GB-mes en Irlanda y 0,0245 en Frankfurt. No encontrado para eu-south-2. — [impossiblecloud](https://www.impossiblecloud.com/magazine/cheapest-s3-storage-vs-aws-europe-2026) [agregador, con interés comercial]
- KMS (precio por clave al mes) y ALB (hora + LCU): no confirmados en búsquedas. A verificar en las páginas oficiales.

**Créditos para startups (2026; todo [agregador], a verificar en los programas oficiales)**
- AWS Activate: nivel Founders autoservicio de 1.000-5.000 USD. Nivel Portfolio hasta 100.000 USD (otra fuente dice 200.000), que requiere un Org ID de aceleradora o VC. — [guptadeepak](https://guptadeepak.com/aws-activate-vs-microsoft-for-startups-vs-google-for-startups-2026-who-each-one-is-actually-for/); [hub.causo.ai](https://hub.causo.ai/guides/startup-cloud-credits-compared-2026)
- Google for Startups Cloud: nivel Start de 2.000 USD. Los niveles Scale (200.000) y AI (350.000) exigen financiación de capital o VC. — [guptadeepak](https://guptadeepak.com/aws-activate-vs-microsoft-for-startups-vs-google-for-startups-2026-who-each-one-is-actually-for/); [agentdeals](https://agentdeals.dev/startup-credits)
- Microsoft for Startups: unos 5.000 USD en el nivel de entrada y hasta 150.000 de forma progresiva o con red de inversores. — mismas fuentes
- Los créditos suelen caducar a los 12 meses y después se factura con normalidad. — [guptadeepak](https://guptadeepak.com/startup-offers/guides/aws-activate)

**Certificaciones ENS / ISO**
- AWS tiene certificación ENS Alto auditada por BDO España. Los posts del blog de seguridad de AWS citan sucesivamente 29, 105, 149 y 166 servicios en alcance. — [AWS ENS](https://aws.amazon.com/compliance/esquema-nacional-de-seguridad); [AWS blog 166 servicios](https://aws.amazon.com/blogs/security/aws-achieves-spains-ens-high-certification-across-166-services) [oficial]
- Microsoft amplió el ENS Alto a 300 servicios y 66 regiones (nota sin fecha visible; la primera certificación es de 2016). — [Microsoft News](https://news.microsoft.com/source/emea/features/microsoft-eleva-a-300-sus-servicios-y-66-regiones-cloud-con-certificacion-alta-del-esquema-nacional-de-seguridad-y-refuerza-su-oferta-de-nube-soberana/?lang=es) [oficial]
- Google Cloud declara cumplir el ENS nivel Alto (RD 311/2022). No se ha confirmado que europe-southwest1 esté expresamente en el alcance. Opsio, un tercero, decía que GCP estaba "en proceso", lo que contradice a Google y está probablemente desactualizado. — [Google Cloud ENS](https://cloud.google.com/security/compliance/ens?hl=en) [oficial]; [Opsio](https://opsiocloud.com/es/servicios-cloud-espana/) [agregador]
- Error en Opsio: sitúa AWS eu-south-2 en Madrid. Según la información pública de AWS, la región Europe (Spain) está en Aragón. No se ha confirmado con fuente en esta sesión; a verificar.

**CLOUD Act y nube soberana 2026**
- AWS European Sovereign Cloud: GA anunciada el 15/01/2026, con primera región eusc-de-east-1 en Brandenburgo. Es física y lógicamente separada del resto de AWS, con gestión y consejo asesor propios en la UE. Inversión de 7.800 M EUR hasta 2040. Hay Local Zones soberanas previstas en Bélgica, Países Bajos y Portugal; España no aparece. — [Amazon press](https://press.aboutamazon.com/aws/2026/1/aws-launches-aws-european-sovereign-cloud-and-announces-expansion-across-europe) [oficial]; [InfoQ](https://www.infoq.com/news/2026/01/aws-european-sovereign-cloud)
- Catálogo de servicios de la ESC: una fuente previa al lanzamiento hablaba de ~90 servicios frente a más de 240 en AWS normal; otra afirma que está todo el portafolio. Contradicción; a verificar. Los precios de la ESC frente a eu-central-1 no se encontraron. — [scalefactory](https://scalefactory.com/blog/2025/10/21/aws-european-sovereign-cloud); [towardsthecloud](https://towardsthecloud.com/blog/aws-european-sovereign-cloud)
- Microsoft (Francia) reconoció ante el Senado francés y en tribunales (julio de 2025) que no puede garantizar plenamente que los datos de la UE estén a salvo de peticiones bajo el CLOUD Act. Su respuesta soberana es Azure Local, operado por un socio de confianza. — [kiteworks](https://www.kiteworks.com/es/gestion-de-riesgos-de-ciberseguridad/paquete-soberania-tecnologica-ue-cloud-act/) [proveedor con interés]; [itdaily](https://itdaily.com/news/cloud/microsoft-strengthens-sovereign-cloud-with-new-features-and-belgian-datacenter)
- Google opera su modelo soberano mediante socios: T-Systems en Alemania (custodio de las claves) y S3NS en Francia (SecNumCloud). No se encontró una oferta específica para España. — [akave](https://akave.com/blog/the-2026-data-sovereignty-reckoning) [proveedor con interés]
- Wasabi es una empresa estadounidense; usar una región en Frankfurt o Ámsterdam no la aísla por sí misma de citaciones de EE. UU. — [danubedata](https://danubedata.ro/blog/wasabi-alternatives-europe-pricing-2026) [agregador]

### Inferences
- **Estimación AWS eu-south-2/Frankfurt para 1-3 clientes** (suma de las cifras anteriores; sin EBS, ALB, KMS, CloudWatch de pago ni IVA): EC2 t4g.medium ~27 + RDS micro Single-AZ ~14 + IPv4 ~3,65 + S3 (≤30 GB ≈ 0,7) ≈ **45 USD/mes**, más almacenamiento EBS/RDS (a verificar). Con un ALB (precio a verificar) y RDS Multi-AZ (~27) la cifra sube a unos **70-90 USD/mes**. Si se añade un NAT Gateway por error, son +33 USD/mes por AZ.
- **10 clientes**: es probable que haya que subir a t4g.large (~0,0736 USD/h ≈ 54 USD/mes según [ec2db](https://ec2db.pages.dev/instances/t4g.large)) por el OCR de CPU, y quizá a RDS small/medium. Estimación: 100-150 USD/mes (a verificar con la calculadora).
- **30 clientes**: 2 VM o una más grande, más ALB, RDS Multi-AZ y unos 100-200 GB en S3 (~2,5-5 USD). Plausiblemente 200-350 USD/mes, aunque es una estimación muy aproximada que no está respaldada por una cotización oficial.
- **Hetzner equivalente**: CX33 8,99 + IPv4 0,50 + Storage Box 3,20 ≈ **12,7 EUR/mes** con 1-3 clientes. Con 30 clientes, 2-3 VM más grandes y quizá PostgreSQL autogestionado: decenas de EUR. La diferencia es de 4 a 8 veces a favor del VPS hasta los 30 clientes.
- **El hiperescalar empieza a tener sentido** si un cliente o una licitación exige ENS Alto certificado, o un proveedor con ISO 27001 y región en España; si se consiguen créditos (por ejemplo 5.000 USD de Activate o Microsoft, que cubrirían más de un año de la configuración mínima); o cuando el coste de operar PostgreSQL con HA y backups propios supere en horas de trabajo la diferencia de precio. Para despachos contables privados el ENS no es obligatorio (aplica al sector público y a sus proveedores), aunque puede servir como argumento de venta.
- Trampas típicas en AWS para equipos pequeños: el NAT Gateway (que se puede evitar con subredes públicas, IPv6 o VPC endpoints), el cobro de cada IPv4, el ALB de coste fijo, los datos entre AZ, los logs de CloudWatch y los snapshots que se olvidan. En Hetzner, la trampa es la subida de 2026 en CPX/CCX y que el CX "cost-optimized" tiene disponibilidad limitada ([vincentschmalbach](https://www.vincentschmalbach.com/hetzner-cheap-cloud-unavailable-price-increases/)).

### Gaps
- No se obtuvieron precios oficiales de eu-south-2 (EC2, RDS, S3, ALB, KMS, Secrets Manager, CloudWatch), Azure Spain Central (B2s, Flexible Server, Key Vault, Load Balancer) ni GCP Madrid (Cloud SQL, Cloud Storage, LB, Secret Manager) porque WebFetch estaba bloqueado. Hay que comprobarlos con las calculadoras oficiales.
- El precio por clave de KMS y el precio por hora de ALB/Application Gateway/Cloud Load Balancing no se confirmaron.
- No se encontraron precios ni la lista definitiva de servicios de la AWS European Sovereign Cloud, ni si existe una oferta de nube soberana con presencia en España (de Microsoft, Google o socios).
- Certificaciones ENS/ISO 27001 de Hetzner, OVH y Scaleway: no investigadas en esta tanda.
- No se pudo confirmar desde una fuente oficial el contenido exacto del alcance del ENS de Google en la región de Madrid.

## Pregunta 2: ¿Cuál es la copia off-site cifrada más barata y robusta en otro centro de datos de la UE para decenas o cientos de GB?

### Takeaway
Para 50-300 GB, las opciones más baratas son Scaleway u OVH Object Storage (unos 0,012-0,015 EUR/GB-mes; OVH sin egress desde el 1/1/2026; ambos con Object Lock en S3) y Hetzner Storage Box BX11 (3,20 EUR/mes fijos por 1 TB, sin Object Lock). Wasabi no compensa por debajo de 1 TB, porque cobra un mínimo de 1 TB y 90 días. B2 es barato (6,95 USD/TB) y tiene Object Lock, pero la región EU y sus condiciones no se confirmaron. Recomendación: cifrar en el cliente (restic, borg o kopia), copia primaria a otro proveedor de la UE con Object Lock (Scaleway o OVH) y, opcionalmente, una segunda copia barata en una Storage Box.

### Cited Findings
- **Hetzner Storage Box BX11 (1 TB)**: 3,20 EUR/mes + IVA, es decir 3,81 EUR con el 19 % de IVA alemán. Datos de octubre de 2025; no se encontró subida de Storage Box en 2026, aunque Hetzner subió otros productos ese año. BX21 (5 TB): ~11,90 EUR/mes, según una fuente de junio de 2026. — [whtop](https://www.whtop.com/amp/plans/hetzner.com/128269) [agregador]; [remote-backups](https://remote-backups.com/comparison/hetzner-storage-box) [agregador]; [cloud-cost-557](https://cloud-cost-557.pages.dev/provider/hetzner/) [agregador]. A verificar en [hetzner.com/storage-box](https://www.hetzner.com/storage-box) [oficial, no accesible].
- **Scaleway** [oficial, página de precios vía fragmento]: Multi-AZ Standard ~0,0146 EUR/GB-mes; One Zone-IA ~0,012; Glacier ~0,002 (el paso a Glacier es gratis y restaurar cuesta 0,009 EUR/GB). Egress: 75 GB/mes gratis y después 0,01 EUR/GB. Peticiones e ingress incluidos. Un blog de 2026 da 0,0105 EUR/GB, en contradicción con la página oficial. Los 75 GB de almacenamiento gratuito ya no existen (solo queda el egress gratuito, según un foro de 2023). — [Scaleway pricing](https://www.scaleway.com/fr/tarifs/storage) [oficial]; [lowendspirit](https://lowendspirit.com/discussion/6958) [foro]
- **OVHcloud Object Storage**: sin tarifas de egress desde el 1/1/2026 (salvo en Asia-Pacífico, según un tercero). El FAQ oficial da tramos por GB-hora: 0,00001917/GB-h ≈ 14 EUR/TB-mes en el primer tramo (hasta ~50 TiB) y ≈ 12,5 en el segundo. Otros agregadores dicen 0,0119 EUR/GB o ~0,0081 USD/GB (contradicción). Se factura por GiB-hora. OVH recomienda Object Lock para backups, pero no está disponible en Cold Archive. Cold Archive: ~0,0013 EUR/GB-mes y 0,01 EUR/GB de exportación (precio de lanzamiento, probablemente antiguo). — [OVH S3 FAQ](https://docs.ovhcloud.com/en/guides/storage-and-backup/object-storage/s3-faq) [oficial]; [us.ovhcloud.com](https://us.ovhcloud.com/public-cloud/object-storage) [oficial]; [european-alternatives](https://european-alternatives.eu/product/ovh-cloud-object-storage) [agregador]; [ComputerWeekly](https://www.computerweekly.com/news/366537215/OVHcloud-aims-to-bring-Glacier-like-cloud-archive-to-Europe)
- **Backblaze B2**: 6,95 USD/TB-mes. Egress gratis hasta 3 veces el almacenamiento medio mensual y 0,01 USD/GB por encima. Object Lock en modos governance y compliance, con legal hold, vía la API S3. Los agregadores no confirman el precio ni la existencia de la región EU Central (Ámsterdam): a verificar. — [upstash, oct. 2026](https://upstash.com/blog/backblaze-b2-pricing-explained-2026.md) [agregador]; [egresscost, sept. 2026](https://egresscost.com/backblaze-b2) [agregador]
- **Wasabi**: el FAQ oficial cita 7,99 USD/TB-mes (pago por uso en EE. UU. y UE), frente a los 6,99 que repiten muchas comparativas. Una fuente señala el cambio el 1/7/2026. Tiene mínimo de 1 TB al mes y mínimo de 90 días (se cobra el borrado anticipado). El egress es "gratis" mientras no supere el almacenamiento activo, y si se supera de forma recurrente pueden limitar el servicio. Regiones UE: Londres, Frankfurt, Ámsterdam y París. — [Wasabi FAQ](https://wasabi.com/pricing/faq) [oficial]; [leanopstech](https://leanopstech.com/blog/wasabi-pricing-2026/) [agregador]; [egresscost](https://egresscost.com/wasabi) [agregador]
- **AWS S3**: Standard a 0,0245 USD/GB-mes en Frankfurt. Para Glacier Deep Archive las fuentes no coinciden: unas dicen "0,0099/GB" (probable errata de 0,00099, el precio de us-east-1) y otra da 0,0018 en Frankfurt, con mínimo de 180 días. Egress a 0,09 USD/GB después de los 100 GB gratuitos. — [impossiblecloud](https://www.impossiblecloud.com/magazine/cheapest-s3-storage-vs-aws-europe-2026) [agregador]; [usage.ai](https://www.usage.ai/blogs/aws/storage-cost/glacier-deep-archive-pricing/) [agregador]; [AWS free tier](https://aws.amazon.com/blogs/aws/aws-free-tier-data-transfer-expansion-100-gb-from-regions-and-1-tb-from-amazon-cloudfront-per-month) [oficial]

### Inferences
- **Coste mensual aproximado con 100 GB / 300 GB** (calculado a partir de las cifras anteriores; sin IVA):
  - Scaleway Multi-AZ: 1,46 / 4,38 EUR. One Zone-IA: 1,20 / 3,60 EUR. Glacier: 0,20 / 0,60 EUR (más 0,009 EUR/GB al restaurar).
  - OVH (~14 EUR/TB): ~1,4 / ~4,1 EUR, con restauración gratis.
  - Hetzner BX11: 3,20 EUR fijos hasta 1 TB.
  - B2: ~0,70 / ~2,1 USD, con restauración gratis hasta 3 veces el volumen.
  - Wasabi: 7,99 USD como mínimo (se factura 1 TB) en ambos casos.
  - S3 Frankfurt Standard: 2,45 / 7,35 USD, más egress de restauración por encima de 100 GB/mes.
- **Prueba de restauración mensual completa** (por ejemplo, 100 GB): gratis en OVH, B2, Wasabi, S3 (dentro de los 100 GB de free tier) y Hetzner. En Scaleway cuesta unos 0,25 EUR (25 GB por encima de los 75 gratuitos).
- **Inmutabilidad**: Scaleway, OVH, B2, Wasabi y S3 ofrecen Object Lock. La Storage Box es SFTP/Borg sin Object Lock, así que conviene usar borg o restic en modo append-only y sus snapshots (soporte de snapshots y append-only a verificar en la documentación de Hetzner). Es la más barata por TB, pero la menos robusta frente a ransomware que borre con credenciales robadas.
- **3-2-1 para Factucoin**: (1) datos vivos en el VPS; (2) snapshot o backup diario en otro proveedor de la UE con Object Lock en compliance mode (Scaleway en PAR/AMS u OVH en otro DC); (3) opcionalmente, una Storage Box en otra ubicación de Hetzner. Si el primario está en Hetzner, la copia en la Storage Box es del mismo proveedor y no cubre el riesgo de proveedor. Cifrado en el cliente con restic/kopia y claves fuera del proveedor. Para SQLite por cliente, usar la API de backup o `VACUUM INTO` (o Litestream) antes de subir.
- Wasabi y B2 son empresas estadounidenses (aplica el CLOUD Act); con cifrado en el cliente el riesgo se reduce bastante. OVH, Scaleway y Hetzner son europeos.

### Gaps
- Ubicaciones exactas de la Storage Box (FSN, HEL, ¿NBG?), soporte de snapshots y append-only, y posibles cambios de precio en 2026: sin fuente oficial.
- Región EU de B2 y su precio: sin confirmar en 2026.
- Precio por GB oficial actual de OVH en EUR (las cifras se contradicen) y ubicaciones de OVH con Object Lock.
- Precio de S3 en eu-south-2 y precio real de Deep Archive en la UE.

## Pregunta 3: ¿Qué costes ocultos (egress, IPv4, NAT gateways) suelen sorprender a los equipos pequeños?

### Takeaway
En AWS las sorpresas más habituales son el NAT Gateway (~33 USD/mes por AZ más 0,045 USD/GB), el cobro de cada IPv4 pública (3,65 USD/mes), el egress a 0,09 USD/GB a partir de 100 GB y el coste fijo de balanceadores y Multi-AZ. En almacenamiento, los mínimos de Wasabi (1 TB y 90 días), las retenciones mínimas de los tiers de archivo (180 días en Deep Archive) y las tasas de restauración. En Hetzner, la sorpresa de 2026 fueron las subidas de precio y el IPv4 aparte.

### Cited Findings
- IPv4 pública en AWS: 0,005 USD/h por IP, desde el 1/2/2024, incluso sin asociar. — [AWS News Blog](https://aws.amazon.com/blogs/aws/new-aws-public-ipv4-address-charge-public-ip-insights) [oficial]
- NAT Gateway: ~0,045 USD/h + 0,045 USD/GB, horas parciales facturadas completas, y multiplicado por AZ. Varía por región (por ejemplo, 0,062 USD/h en Tokio). — [cloudburn](https://cloudburn.io/blog/aws-nat-gateway-pricing) [agregador]; [awsfundamentals](https://awsfundamentals.com/blog/avoid-nat-gateway-costs) [agregador]
- Egress de AWS: 100 GB/mes gratis a nivel global y luego ~0,09 USD/GB en la UE. — [AWS blog](https://aws.amazon.com/blogs/aws/aws-free-tier-data-transfer-expansion-100-gb-from-regions-and-1-tb-from-amazon-cloudfront-per-month) [oficial]; [cloudzero](https://www.cloudzero.com/blog/aws-egress-costs) [agregador]
- Wasabi: mínimo de 1 TB y cargo por borrado antes de 90 días; egress limitado al volumen almacenado como política. — [Wasabi FAQ](https://wasabi.com/pricing/faq) [oficial]
- Deep Archive: mínimo de 180 días. — [usage.ai](https://www.usage.ai/blogs/aws/storage-cost/glacier-deep-archive-pricing/) [agregador]
- Scaleway: el egress entre regiones también se cobra (después de los 75 GB gratuitos, a 0,01 EUR/GB). — [Scaleway pricing](https://www.scaleway.com/fr/tarifs/storage) [oficial]
- Hetzner: IPv4 a 0,50 EUR/mes aparte; repricing de junio de 2026 en CPX/CCX de hasta +176 %. — [wz-it](https://wz-it.com/en/blog/hetzner-price-increase-june-2026-cpx-ccx-alternatives/) [agregador]
- Los créditos de startup caducan, normalmente a los 12 meses, y la factura aparece de golpe. — [guptadeepak](https://guptadeepak.com/startup-offers/guides/aws-activate) [agregador]

### Inferences
- Una arquitectura AWS de "manual" (VPC con subredes privadas en 2 AZ, 2 NAT, ALB, RDS Multi-AZ) puede costar más de 100 USD/mes en red y alta disponibilidad antes de servir a un solo cliente. Para 1-10 clientes, lo razonable es una sola VM en subred pública con security groups, sin NAT, y RDS Single-AZ o SQLite con backups.
- El egress apenas importa en esta carga (facturas en PDF, pocos usuarios por despacho). Sí importa en restauraciones y migraciones de proveedor; por eso OVH (egress cero) o B2 (3 veces) son ventajosos como destino de backups.

### Gaps
- Coste de CloudWatch, Azure Monitor y Cloud Logging en un volumen pequeño, transferencia entre AZ y precio de Secrets Manager o Key Vault: no confirmados.
- Precio de IPv4 en Azure y GCP: no investigado.
