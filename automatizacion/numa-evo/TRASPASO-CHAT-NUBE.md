# Traspaso del chat de la nube (04-06 nov 2026) a Numa Evo local

> **Para tu Claude local:** lee esto e incorpóralo a `docs/CONTEXTO-NUMA.md` (decisiones y conocimiento) y a `ESTADO.md` (pendientes). No dupliques lo que ya esté. No borres nada: deja también este archivo como referencia en `docs/informes/`.

## 1. Cómo trabajamos a partir de ahora
- **Un solo sitio: la terminal del Mac**, dentro de `~/Desktop/automatization/Numa Evo/`. La memoria vive en archivos, no en el chat.
- **Al final de cada sesión:** actualizar `ESTADO.md` y, si hay decisiones nuevas, `docs/CONTEXTO-NUMA.md`.
- **Retomar:** `claude --continue` (último chat) o `claude --resume` (elegir).
- **Factory sí:** lo importante (formulario real, servidor, interfaz del software, cualquier cosa con datos o que vean clientes por primera vez). **Factory no:** retoques pequeños de texto o fallos visuales, si Adrián lo dice.
- **Modelo:** Sonnet para tareas normales; Opus para lo que piense más. Plan Pro: mirar `/usage` antes de cambios de riesgo alto.

## 2. El flujo de una factura (para explicarlo y para diseñar pantallas)
1. Llega la factura (la gestoría la sube).
2. **Leer** en cascada: texto del PDF → OCR (RapidOCR) → OCR de rescate → **IA solo si lo anterior falla** (Haiku en Bedrock UE, céntimos).
3. **Contabilizar SIN IA**, con reglas: reglas de esa gestoría → su histórico de Sage → reglas generales del PGC → si nada encaja, «sin propuesta» y a revisión.
4. Excel (o pantalla) de revisión con **semáforo** verde/ámbar/rojo.
5. La gestoría corrige.
6. **Cada corrección pasa a regla de esa gestoría** (hoy lo hace Alex con Claude Code; Alex está haciendo que lo haga el programa solo).
7. Tras su «sí», XML para su Sage. **Nunca** importamos nosotros en Sage.
- Claude (Opus/Sonnet con Claude Code) va **por detrás**: revisa reglas, junta las repetidas, mejora el sistema. No toca facturas en directo.

## 3. Servidor (resumen; detalle en `docs/informes/INVESTIGACION-SERVIDOR.md`)
- VPS Hetzner CX33 (Alemania), Linux, Docker, ≈10-13 €/mes. Plan B: OVH VPS-2 (7,21 €).
- **No hace falta Mac**: Apple Vision (OCR de rescate) solo existe en macOS, pero se sustituye por un 2.º OCR gratis en Linux o por la IA con imagen. Alex mide la pérdida con `FAC_VISION=0`. Si fuera mucha: Mac alquilado en Scaleway solo en la semana de cierre.
- **Pentest = puerta**: ninguna factura real entra sin pasarlo.
- Lo legal: contrato de encargo (art. 28) con cada gestoría, subencargados autorizados por escrito, IA en la UE, plan de brechas (<72 h). Revisión profesional antes de abrir a desconocidos.

## 4. Competencia (detalle en `docs/informes/COMPETENCIA-NUMA.md`)
- Leer y proponer asiento ya lo venden muchos y barato (Copilot 0-99 €/mes, Contabilify, Inmatic, Dijit, Holded para asesorías, Esphera.ai). **AutoApunte** ya vende servicio a medida para asesorías.
- Nuestro hueco **por demostrar**: criterio de cada gestoría (no solo por proveedor), arrancar con su histórico de Sage, sentarnos con ellos, trabajar con su Sage/A3.
- **No prometer «datos en vuestra oficina»**: decir por escrito dónde está cada dato (UE, contrato, proveedores).

## 5. Formulario de contacto de la web
- Hoy es `mailto:` con dirección falsa → no sirve hasta tener buzón real, y aun así falla si el visitante no tiene programa de correo.
- **Decisión recomendada:** (1) **receptor propio en el servidor Hetzner** (programa pequeño que recibe el formulario y avisa por correo/móvil; anti-spam con trampa invisible y límite de envíos; ajustar CSP `form-action`). Hacerlo **con Factory y riesgo alto** porque recoge datos personales. Sirve además como el «servidor de juguete» que pedía la tarea del servidor. (2) **Botón de WhatsApp** con mensaje prellenado como segunda vía.
- Alternativa rápida descartada por ahora: servicio de formularios (Tally u otro): añade un tercero.

## 6. Lecciones de la Factory (de los cambios 001-003)
- Nombrar el cambio sin número (`unificar-tono`): la Factory pone el número.
- Antes de archivar, corregir `tasks.md` y el spec para que digan lo que de verdad se fusionó.
- Los revisores a veces no escribían su archivo: causa, la regla genérica de «no crear informes»; arreglado en `.claude/skills/factory/SKILL.md` (feb2ab8). Si vuelve a pasar, que el revisor liste sus herramientas.
- Riesgo bajo = solo revisor de código; medio = + UX y UI; alto = + seguridad (Semgrep, Gitleaks, Trivy).
- Caché: nombres estables (`styles.css`, `main.js`) con `Cache-Control: no-cache`; fuentes e imágenes con caché larga (si cambian, cambiar el nombre).

## 7. Prioridades (visitas a Toro y al padre de Alfredo, 10-11 nov)
1. Probar Inmatic, Copilot y Dijit con ~15 facturas inventadas (plan en el informe de competencia).
2. Plantilla de contrato de encargo para el piloto (V19).
3. Demo con ~30 facturas inventadas y Excel con semáforo (con Alex).
4. Guion de 10 minutos y presentación.
5. Después: formulario con receptor propio (punto 5) y la **interfaz de revisión del software** (T11): maquetas con datos inventados en `app/`, sin tocar `web/` ni el motor de Alex.

## 8. Pendientes de la web (ya en ESTADO.md; comprobar)
- Revisar en móvil real el desplegable de «Vuestros datos, por escrito».
- Buzón real, hosting con cabeceras de `docs/CABECERAS.md`, segunda vía de contacto, texto legal de `privacidad.html` por un profesional.
