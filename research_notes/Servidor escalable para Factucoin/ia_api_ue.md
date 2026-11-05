# Opciones de API LLM para facturas con datos personales (UE/RGPD) — notas a 5-nov-2026

Alcance: último paso de una cascada OCR (facturas difíciles: fotos, tickets, con imagen). Rol: sub-encargado de un encargado (art. 28 RGPD). Fecha de investigación: 2026-11-05.
Nota de método: WebFetch funcionó para platform.claude.com (fuente oficial leída íntegra). openai.com y mistral.ai NO resuelven en este entorno (bloqueados por la red de la sesión) → precios de OpenAI y Mistral proceden de agregadores vía WebSearch y se marcan "agregador / a verificar". No se pudo leer azure.microsoft.com, aws.amazon.com/bedrock/pricing ni cloud.google.com pricing (no intentado por presupuesto; los snippets de búsqueda no mostraban cifras).

## 1. Notas por proveedor (precios, residencia UE, ZDR, entrenamiento, DPA, subencargados, SCC/DPF)

### Takeaway
Los precios de Claude que dio el usuario están confirmados en la página oficial (Haiku 5.5 $0.10/$0.50, Sonnet 5.5 $2/$10, Opus 5.5 $4/$20). Pero la API directa de Anthropic NO tiene opción de inferencia en la UE: `inference_geo` solo acepta "global" y "us", y la workspace geo solo "us". Para que la inferencia de Claude se quede en la UE hay que ir por Bedrock o Vertex (Google managed) con endpoints regionales o perfiles geográficos UE, con su propio precio. OpenAI (proyectos con región Europa) y Mistral (UE por defecto) sí ofrecen procesamiento en la UE desde su API directa.

### Cited Findings

**Anthropic Claude API (1P) — fuente oficial, leída el 2026-11-05**
- Precios por MTok (entrada / salida): Claude Haiku 5.5 $0.10 / $0.50 (prompts ≤100k tokens; >100k: $0.50 / $2.50); Claude Sonnet 5.5 $2 / $10; Claude Opus 5.5 $4 / $20; Claude Haiku 4.5 $1 / $5; Sonnet 5 $2 / $10 (con nota al pie 3, posible precio introductorio). Lectura de caché: Haiku 5.5 $0.01, Sonnet 5.5 $0.10, Opus 5.5 $0.20/MTok. — [Claude pricing (oficial)](https://platform.claude.com/docs/en/about-claude/pricing)
- Batch API: 50% de descuento en entrada y salida (Haiku 5.5 batch $0.05 / $0.25; Sonnet 5.5 $1 / $5; Opus 5.5 $2 / $10). Los descuentos se acumulan con caché y con el multiplicador de residencia. — [Claude pricing (oficial)](https://platform.claude.com/docs/en/about-claude/pricing)
- `inference_geo`: valores disponibles solo `"global"` (por defecto, "cualquier geografía disponible") y `"us"`. "Current limitations: Inference geo: Only "us" and "global" are available. Workspace geo: Only "us" is currently available." Soportado en Claude 4.6 y posteriores, incluido Haiku 5.5. Haiku 4.5 y anteriores devuelven 400 si se envía. — [Data residency (oficial)](https://platform.claude.com/docs/en/manage-claude/data-residency)
- Precio de `inference_geo: "us"`: 1,1x en todas las categorías de tokens. Global: precio estándar. — [Data residency (oficial)](https://platform.claude.com/docs/en/manage-claude/data-residency)
- En Bedrock y en Claude on Google Cloud (Google managed), la región de inferencia la determina el endpoint/perfil de inferencia y `inference_geo` no aplica; tienen "independent regional pricing". — [Data residency (oficial)](https://platform.claude.com/docs/en/manage-claude/data-residency); [Claude pricing (oficial)](https://platform.claude.com/docs/en/about-claude/pricing)
- Un post de febrero de 2026 hablaba de una lista de espera para una región de inferencia UE sin país anunciado; la documentación oficial de noviembre de 2026 sigue sin listar "eu" → no está disponible de forma general. — [Claude's daily diary, feb-2026 (no oficial)](https://gsp4dcs2.github.io/claudes-daily-diary/articles/2026/02/2026-02-04.html); [Data residency (oficial)](https://platform.claude.com/docs/en/manage-claude/data-residency)
- Retención y entrenamiento: "Retained data is never used for model training without your express permission." "Conversation content (your prompts and Claude's outputs) is not retained by default; the exception is Covered Models, which require 30-day retention." (Covered Models = Fable 5/5.1, Mythos 5/5.1; Haiku/Sonnet/Opus 5.5 no lo son.) — [API and data retention (oficial)](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- ZDR: con ZDR, Anthropic no guarda prompts ni respuestas en reposo después de devolver la respuesta. Se pide a ventas, se habilita por organización y no se extiende sola a otras organizaciones. Disponible también bajo petición en Claude Platform on AWS y en Claude on Google Cloud (Anthropic managed). Hay funciones excluidas (por ejemplo, code execution). `inference_geo` es apto para ZDR. — [API and data retention (oficial)](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- En Bedrock y Google-managed Vertex, el encargado del tratamiento es el proveedor cloud, no Anthropic; la retención la fijan las condiciones de AWS/Google. — [API and data retention (oficial)](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- Coste de imagen: ⌈ancho/28⌉×⌈alto/28⌉ tokens visuales. El nivel de alta resolución (Claude 4.7 y posteriores, lo que debería incluir Haiku 5.5) tiene borde largo máximo de 2.576 px y como máximo 4.784 tokens; el nivel estándar, 1.568 px y 1.568 tokens. Ejemplos en alta resolución: 1092×1092 = 1.521 tokens; 1920×1080 = 2.691; 2000×1500 (3 MP) = 3.888; 4K se reduce a 4.784. La imagen se cobra como tokens de entrada normales. — [Vision (oficial)](https://platform.claude.com/docs/en/build-with-claude/vision)
- DPA: el DPA de Anthropic autoriza los subencargados listados en el Schedule 4 y prevé un mecanismo de aviso de cambios (no se recuperó la lista). — [Anthropic DPA (oficial, fragmento)](https://www.anthropic.com/legal/data-processing-addendum)
- Guías de terceros dicen que el DPA incluye las SCC 2021 en sus módulos 2 (responsable a encargado) y 3 (encargado a encargado), y que Anthropic participa en el DPF. No se confirmó en la lista oficial del DPF. — [compound.law (tercero)](https://compound.law/en-DE/tools/anthropic-scc/); [compound.law DPA (tercero)](https://compound.law/en-DE/tools/anthropic-dpa/)

**Claude vía AWS Bedrock (UE)**
- Los perfiles de inferencia geográficos "EU" enrutan solo dentro de regiones UE: eu-central-1 (Frankfurt), eu-west-3 (París), eu-north-1 (Estocolmo), eu-south-1 (Milán), eu-south-2 (España), eu-west-1 (Irlanda), según la ficha de Opus 4.6. — [AWS Bedrock model card Opus 4.6](https://docs.aws.eu/bedrock/latest/userguide/model-card-anthropic-claude-opus-4-6.html)
- AWS: "no additional routing cost for using cross-Region inference"; el precio se calcula según la región desde la que se llama al perfil. — [AWS cross-region inference](https://docs.aws.eu/bedrock/latest/userguide/cross-region-inference.html)
- La página heredada de Anthropic sobre Bedrock dice que los endpoints regionales llevan un recargo del 10% frente a los globales (modelos desde Sonnet 4.5, Haiku 4.5 y Opus 4.5). — [Claude on Bedrock legacy (oficial)](https://platform.claude.com/docs/en/build-with-claude/claude-on-amazon-bedrock-legacy); [Claude pricing (oficial)](https://platform.claude.com/docs/en/about-claude/pricing)
- Bedrock: solo admite imágenes en base64, con un máximo de 5 MB por imagen. — [Vision (oficial)](https://platform.claude.com/docs/en/build-with-claude/vision)
- Disponibilidad de Haiku 5.5 en Bedrock UE: a verificar. Las búsquedas solo devolvieron fichas de Haiku 4.5 y de Opus 4.6, 4.7, 4.8 y 5.
- Además existe "Claude Platform on AWS" (operado por Anthropic), pero su workspace geo es "us" y `inference_geo` solo ofrece us o global, así que no sirve para tener residencia UE. — [Data residency (oficial)](https://platform.claude.com/docs/en/manage-claude/data-residency)

**Claude vía Google Vertex (UE)**
- Haiku 4.5 tiene endpoint regional europe-west1 (Bélgica) y también multirregión EU. — [Google Vertex Haiku 4.5 (oficial)](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/partner-models/claude/haiku-4-5); [Vertex data residency (oficial)](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/data-residency)
- Google-managed ofrece endpoints globales y multirregión para los modelos nuevos; los regionales solo para Sonnet 4.6 y anteriores. — [Claude pricing (oficial)](https://platform.claude.com/docs/en/about-claude/pricing)
- Un agregador da Haiku 4.5 en Vertex Bélgica a $1,10 / $5,50, lo que cuadra con el +10%. — [requesty (agregador)](https://www.requesty.ai/models-new/vertex/claude-haiku-4-5-europe-west1)
- Haiku 5.5 en Vertex UE: a verificar, no se encontró.

**OpenAI API / Azure OpenAI (UE)**
- Residencia de datos en Europa: se elige la región Europa al crear un proyecto nuevo; los proyectos existentes no se pueden cambiar. Las peticiones de esos proyectos se tratan en la región con zero data retention ("model requests and responses are not stored at rest"). — [OpenAI, introducing data residency in Europe (oficial)](https://openai.com/index/introducing-data-residency-in-europe/)
- Contradicción: una guía de terceros dice que hace falta aprobación para el abuse monitoring modificado o para ZDR, y que los datos de sistema pueden tratarse fuera de la región. Hay que confirmarlo con ventas. — [wavect (tercero)](https://wavect.io/blog/eu-data-residency-ai-apps-2026/)
- Esa misma guía menciona un recargo en 2026 para los endpoints con residencia en modelos nuevos, sin dar cifras: a verificar. — [wavect (tercero)](https://wavect.io/blog/eu-data-residency-ai-apps-2026/)
- Precios (agregadores, sin confirmar en la página oficial): GPT-5.4 mini $0.75 / $4.50 (verificado el 2026-07-24 por el agregador); GPT-5.4 nano $0.20 / $1.25 (CostBench, comprobado el 2026-10-10). CostBench lista también "gpt-6-luna" a $0.10 / $0.50, nombre no confirmado. — [trevorfox (agregador)](https://trevorfox.com/tools/calculators/llm-cost/openai/gpt-5.4-mini/); [costbench (agregador)](https://costbench.com/software/llm-api-providers/openai-api/)
- Azure OpenAI tiene despliegues Global, Data Zone (EU/US) y Regional. Un agregador dice que la Data Zone EU cuesta 1,2x el Global Standard, otro dice que mantiene el mismo precio. No se pudieron ver cifras oficiales: a verificar. — [Azure OpenAI pricing (oficial, sin cifras en snippet)](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service); [benchlm (agregador)](https://benchlm.ai/azure/llm-pricing)
- No usar datos de la API para entrenar, DPA, subencargados y DPF de OpenAI/Microsoft: no se verificaron en esta sesión → a verificar en openai.com/policies y en el Microsoft Products and Services DPA.

**Mistral AI (Francia)**
- Precios (agregadores): Mistral Small 4 $0.15 / $0.60; otro agregador da "Mistral Small" a $0.20 / $0.60 (1-sep-2026); Small 3.2 $0.10 / $0.30 (anterior); Mistral Medium 3.5 (lanzado el 30-abr-2026) $1.50 / $7.50; Medium 3 $0.40 / $2.00. — [pricepertoken (agregador)](https://pricepertoken.com/pricing-page/model/mistral-ai-mistral-small); [anotherwrapper Medium 3.5 (agregador)](https://anotherwrapper.com/llm-pricing/mistral-medium-3-5); [cloudzero (agregador)](https://www.cloudzero.com/blog/mistral-api-pricing)
- Alojamiento en la UE por defecto (endpoint US solo si se elige). Algunas funciones pueden transferir datos fuera de la UE a subencargados bajo SCC del art. 46. — [waimakers (tercero)](https://www.waimakers.com/en/resources/gdpr-compliance/mistral-ai)
- Retención por defecto de 30 días para abuse monitoring. ZDR existe, pero no es autoservicio: se pide por escrito con justificación y Mistral puede aprobarlo o denegarlo. — [anarlog (tercero)](https://anarlog.so/blog/mistral-data-retention-policy); [developersdigest (tercero)](https://www.developersdigest.tech/models/data-retention/mistral)
- Entrenamiento: las fuentes se contradicen. Según el resumen de sus Commercial Terms, Mistral no entrena con datos de clientes salvo opt-in, o cuando el cliente no ha hecho opt-out en productos que son opt-in por defecto. Hay que revisarlo en legal.mistral.ai. — [waimakers (tercero)](https://www.waimakers.com/en/resources/ai-data-security/mistral-ai)
- Hay DPA para La Plateforme (legal.mistral.ai), no leído directamente. — [waimakers (tercero)](https://www.waimakers.com/en/resources/gdpr-compliance/mistral-ai)

**EU-US Data Privacy Framework (estado en 2026)**
- El Tribunal General desestimó el recurso Latombe (T-553/23) el 3-sep-2025. Latombe recurrió en casación ante el TJUE el 31-oct-2025 (C-703/25 P). — [WilmerHale (dic-2025)](https://www.wilmerhale.com/insights/blogs/wilmerhale-privacy-and-cybersecurity-law/20251201-european-court-of-justice-to-review-challenge-to-eu-us-data-privacy-framework); [digitalpolicyalert](https://digitalpolicyalert.org/event/35459-latombe-filed-appeal-against-general-court-dismissal-of-challenge-to-european-unionunited-states-data-protection-framework-adequacy-decision-in-latombe-v-commission)
- En febrero de 2026, la DPA noruega decía que el DPF sigue vigente y recomendaba tener una estrategia de salida. — [streamlex DPF tracker](https://streamlex.eu/resources/dpf-developments-tracker/)
- Next.ink tituló que el recurso de Latombe "échoue devant la CJUE", pero el snippet no tenía fecha y puede referirse al Tribunal General en 2025. Estado de la casación a noviembre de 2026: a verificar en curia.europa.eu (C-703/25 P). — [next.ink](https://next.ink/198038/echange-de-donnees-avec-les-usa-le-recours-du-depute-philippe-latombe-echoue-devant-la-cjue/)

### Inferences
- Para el sub-encargado, la API directa de Anthropic implica una transferencia internacional: la inferencia es "global" o "us" y la workspace geo es "us". Se cubriría con DPF/SCC más un TIA, y conviene pedir ZDR. Es legal con garantías, pero no deja los datos en la UE.
- Bedrock con perfil geográfico EU (que incluye eu-south-2, España) o Vertex en europe-west1 o multirregión EU mantiene la inferencia en la UE. AWS/Google pasan a ser el encargado/subencargado, y suelen estar ya en la lista de subencargados de muchas SaaS. La contrapartida es que el modelo barato disponible en la UE podría ser Haiku 4.5 ($1/$5 +10%), unas 10 veces más caro que Haiku 5.5, si Haiku 5.5 no está en regiones UE (a verificar).
- OpenAI con proyecto en región Europa combina procesamiento en la UE y ZDR, pero la empresa sigue sometida a la ley estadounidense (CLOUD Act). Mistral es de la UE y tiene residencia UE por defecto, pero el ZDR requiere aprobación.

### Gaps
- Precios oficiales de OpenAI, Azure (Data Zone EU), Bedrock (región UE) y Vertex (UE) no confirmados: los dominios estaban bloqueados o los snippets no traían cifras.
- Disponibilidad de Haiku 5.5 y Sonnet 5.5 en regiones UE de Bedrock y Vertex: sin confirmar.
- Listas de subencargados de Anthropic (Schedule 4), OpenAI y Mistral: no recuperadas.
- Certificación DPF de Anthropic y OpenAI en dataprivacyframework.gov: sin verificar.
- Coste de imagen en OpenAI y Mistral: no investigado.

## 2. Coste por factura y por mes (supuestos explícitos)

### Takeaway
Con 3.000 tokens de entrada y 500 de salida, Claude Haiku 5.5 cuesta unos $0,00055 por factura: $27,50 al mes en el peor caso (50.000 facturas, 100% al LLM). Incluso Sonnet 5.5 en ese peor caso son $550 al mes. El coste del LLM es marginal frente a las diferencias de riesgo legal entre opciones.

### Cited Findings
- Fórmula: coste = 3.000 × precio_entrada/1e6 + 500 × precio_salida/1e6. Precios de Claude de la [página oficial (2026-11-05)](https://platform.claude.com/docs/en/about-claude/pricing). OpenAI y Mistral de agregadores (ver sección 1). Haiku 4.5 regional +10%, inferido de la [página oficial de Anthropic sobre Bedrock](https://platform.claude.com/docs/en/build-with-claude/claude-on-amazon-bedrock-legacy) y de [requesty](https://www.requesty.ai/models-new/vertex/claude-haiku-4-5-europe-west1).
- Una foto de 3 MP cuesta unos 3.888 tokens en los modelos de alta resolución; una imagen de unos 1 MP, unos 1.300-1.500. — [Vision (oficial)](https://platform.claude.com/docs/en/build-with-claude/vision)

Coste mensual en USD (columnas: volumen mensual @ % de facturas que llegan al LLM; facturas al LLM: 1k → 100/300/1.000; 10k → 1.000/3.000/10.000; 50k → 5.000/15.000/50.000):

| Modelo | $/factura | 1k@10% | 1k@30% | 1k@100% | 10k@10% | 10k@30% | 10k@100% | 50k@10% | 50k@30% | 50k@100% |
|---|---|---|---|---|---|---|---|---|---|---|
| Claude Haiku 5.5 (1P, global) — oficial | 0.00055 | 0.05 | 0.16 | 0.55 | 0.55 | 1.65 | 5.50 | 2.75 | 8.25 | 27.50 |
| Claude Haiku 5.5 inference_geo=us (x1,1) — oficial | 0.00061 | 0.06 | 0.18 | 0.61 | 0.61 | 1.82 | 6.05 | 3.03 | 9.08 | 30.25 |
| Claude Sonnet 5.5 — oficial | 0.01100 | 1.10 | 3.30 | 11.00 | 11.00 | 33.00 | 110.00 | 55.00 | 165.00 | 550.00 |
| Claude Opus 5.5 — oficial | 0.02200 | 2.20 | 6.60 | 22.00 | 22.00 | 66.00 | 220.00 | 110.00 | 330.00 | 1,100.00 |
| Claude Haiku 4.5 +10% regional UE (Bedrock/Vertex) — a verificar | 0.00605 | 0.60 | 1.81 | 6.05 | 6.05 | 18.15 | 60.50 | 30.25 | 90.75 | 302.50 |
| GPT-5.4 mini (agregador, sin recargo UE) | 0.00450 | 0.45 | 1.35 | 4.50 | 4.50 | 13.50 | 45.00 | 22.50 | 67.50 | 225.00 |
| GPT-5.4 nano (agregador, sin recargo UE) | 0.00122 | 0.12 | 0.37 | 1.22 | 1.23 | 3.67 | 12.25 | 6.12 | 18.38 | 61.25 |
| Mistral Small 4 (agregador) | 0.00075 | 0.08 | 0.22 | 0.75 | 0.75 | 2.25 | 7.50 | 3.75 | 11.25 | 37.50 |
| Mistral Medium 3.5 (agregador) | 0.00825 | 0.83 | 2.48 | 8.25 | 8.25 | 24.75 | 82.50 | 41.25 | 123.75 | 412.50 |

### Inferences
- Batch API (-50%) es aplicable si el procesamiento puede ser asíncrono (Anthropic: hasta 24 h). Reduce a la mitad las cifras de Claude.
- Si cada factura lleva una foto de 3 MP más unos 500 tokens de prompt, la entrada real se acerca a 4.400 tokens: la entrada sube alrededor de un 45% y el coste por factura, alrededor de un 25-35% según el modelo. Redimensionar a unos 1.500 px de lado largo deja la imagen en unos 1.500-2.700 tokens.
- El recargo UE de OpenAI y Azure (posiblemente 1,1-1,2x, sin confirmar) no cambia el orden de magnitud.

### Gaps
- Cuántos tokens consume de verdad un ticket típico (depende de la resolución y del prompt): conviene medirlo con el endpoint de conteo de tokens.
- Precio real de Haiku 5.5 en regiones UE de Bedrock y Vertex, si está disponible.

## 3. ¿Qué opción minimiza el riesgo legal (UE, sin entrenamiento, ZDR) a coste aceptable?

### Takeaway
Para minimizar el riesgo con coste bajo, hay dos candidatas. La primera es Claude en AWS Bedrock con perfil geográfico EU (incluye la región de España) o Vertex en la UE: la inferencia se queda en la UE, AWS/Google actúan como encargado y Claude no entrena con los datos. La segunda es Mistral con ZDR aprobado: proveedor de la UE y alojamiento en la UE. La API directa de Anthropic con Haiku 5.5 es la más barata y es ZDR-elegible, pero sin opción UE (solo "global" o "us") implica una transferencia internacional con DPF/SCC. El coste mensual es de decenas a cientos de dólares en todas las opciones.

### Cited Findings
- API directa de Anthropic: solo us/global; los datos no se usan para entrenar sin permiso expreso; el contenido no se retiene por defecto (salvo Covered Models); ZDR bajo petición. — [Data residency (oficial)](https://platform.claude.com/docs/en/manage-claude/data-residency); [API and data retention (oficial)](https://platform.claude.com/docs/en/manage-claude/api-and-data-retention)
- Bedrock EU incluye eu-south-2 (España) entre los destinos del perfil EU. — [AWS model card](https://docs.aws.eu/bedrock/latest/userguide/model-card-anthropic-claude-opus-4-6.html)
- OpenAI, proyectos con región Europa: procesamiento en la región y ZDR. — [OpenAI (oficial)](https://openai.com/index/introducing-data-residency-in-europe/)
- El DPF sigue vigente, pero la casación C-703/25 P está pendiente y las autoridades recomiendan tener un plan de salida. — [streamlex](https://streamlex.eu/resources/dpf-developments-tracker/)

### Inferences
- Ranking de menor a mayor riesgo legal (inferencia propia):
  1. Autoalojado en la UE (sin tercero LLM).
  2. Mistral UE con ZDR, o Bedrock/Vertex con perfil o región UE.
  3. OpenAI con proyecto en región Europa y ZDR, o Azure Data Zone EU.
  4. Anthropic API directa con ZDR e `inference_geo` us/global (transferencia a EE. UU.).
- Para un SaaS español de facturas, Bedrock EU encaja si ya se usa AWS: un DPA de AWS que normalmente ya está firmado y un subencargado conocido. Coste esperado con Haiku 4.5 regional: menos de $305 al mes en el peor caso.
- Alternativa: pedir a Anthropic acceso a la región UE si hay lista de espera (estado a verificar).

### Gaps
- Que AWS/Google no retienen prompts de Bedrock/Vertex ni los usan para entrenar: no se leyó la documentación oficial en esta sesión (es la política habitual conocida, pero hay que verificarlo).
- Si un sub-encargado UE de capital estadounidense (AWS, Google, Microsoft) basta frente a las exigencias de los clientes: es una cuestión de evaluación jurídica.

## 4. ¿Merece la pena autoalojar un modelo de visión abierto con 3-30 tenants?

### Takeaway
Por coste, no. Una GPU en la UE 24/7 cuesta entre unos 184 y 2.000 €/mes, mientras que la API con Haiku 5.5 cuesta menos de 30 $/mes incluso a 50.000 facturas con el 100% al LLM, y Sonnet 5.5 unos 550 $. Solo se justifica si el riesgo legal (datos fuera de terceros) o una exigencia contractual de los clientes pesa más que los costes de operación (ops, actualizaciones, calidad inferior en tickets difíciles).

### Cited Findings
- Hetzner GEX44 (RTX 4000 SFF Ada, 20 GB): 184 €/mes más 79 € de alta, en Falkenstein. Un artículo de octubre de 2026 dice que se redirige al GEX45 y que no está disponible. GEX130 (RTX 6000 Ada, 48 GB): 813-838 €/mes, cifras en conflicto. — [Hetzner GPU (oficial)](https://www.hetzner.com/gpu); [wz-it oct-2026 (tercero)](https://wz-it.com/en/blog/hetzner-gpu-server-comparison/)
- Scaleway: L4 a 0,79 €/h y L40S a 1,47 €/h (comparativa de 2026). Un agregador de octubre de 2026 da L4 $0,88/h, L40S $1,68/h y H100 SXM $3,21/h. — [Qovery 2026 (tercero)](https://www.qovery.com/blog/gpu-pricing-comparison-method-aws-gcp-azure-scaleway-2026); [computeprices (agregador)](https://computeprices.com/compare/ovhcloud-vs-scaleway)
- OVHcloud: H100-380 (1x H100 PCIe 80 GB) a 2,80 €/h (27-jul-2026); L4 unos $1,00/h (octubre de 2026). — [Spheron (tercero)](https://www.spheron.network/blog/ovhcloud-gpu-pricing-2026-h100-cost-and-sovereign-ai/); [computeprices (agregador)](https://computeprices.com/compare/ovhcloud-vs-scaleway)

### Inferences
- Mensual 24/7 (730 h): Scaleway L4 unos 577 €; L40S unos 1.073 €; OVH H100 unos 2.044 €; Hetzner GEX44 184 € (si sigue disponible).
- Punto de equilibrio frente a Haiku 5.5 a $0,00055 por factura: el GEX44 equivale a unas 360.000 facturas al mes procesadas por el LLM, muy por encima de 50.000. Frente a Sonnet 5.5 ($0,011), el GEX44 se amortiza con unas 18.000 facturas al mes al LLM y la L4 de Scaleway con unas 57.000. Cálculo propio, tomando 1 € ≈ 1,08 $ (tipo no verificado).
- Un modelo de unos 7-8B en visión (por ejemplo Qwen-VL 7B) cabe en 20-24 GB. Uno de 32B o más requiere 48-80 GB, es decir, una L40S o una H100.
- Alternativa: una GPU por horas o a demanda en lote (encender solo para procesar colas), o un Mac Studio propio (coste de capital, no investigado).
- Con 3-30 tenants, la API (Bedrock EU, Mistral o Anthropic con ZDR) es más barata y de mejor calidad. Autoalojar tiene sentido como "modo soberano" premium o si los clientes vetan subencargados LLM.

### Gaps
- Precio y disponibilidad oficiales actuales de Scaleway, OVH y Hetzner GEX45: no confirmados en sus páginas.
- Calidad comparada de Qwen-VL, Llama vision y Mistral Small vision frente a Claude Haiku 5.5 en tickets españoles: no investigado.
- Coste de un Mac (M-series) para inferencia: no investigado.
