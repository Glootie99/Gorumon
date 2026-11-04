# Resumen para retomar (conversación anterior, hasta 2026-11-04)

Léelo antes de nada. Responde breve y en español.

## Personas y marcas
- Socios: Adrián (yo, perfil ciberseguridad/OT), Alex (creó el software de facturas, domina Claude Code, plan Max) y Toto.
- **Nodia**: marca paraguas (automatización a medida para negocios de Madrid Norte). Logo: NODIA con la O como brújula (aguja dorada). Paquete en `automatizacion/assets/nodia/marca/`.
- **Numa**: producto para gestorías (lee facturas, propone asientos, el asesor da el visto bueno en Excel, exporta a Sage). Logo: NUMA con la N de cuenta en T. Paquete en `automatizacion/assets/marca/`.

## Dónde está el trabajo real
- Proyecto local de Adrián: `~/Desktop/automatization` → repo privado **Glootie99/nodia-automatization** (rama master). Carpetas: `numa/`, `nodia/`, `openspec/`, `factory/`, `scripts/`, `.claude/`. CLAUDE.md, AGENTS.md y ESTADO.md mandan.
- Web de Nodia (Astro): `~/Desktop/nodia`, repo aparte.
- `deploys/` y Cloudflare (numa-8pp.pages.dev con Access): herramienta **personal** de Adrián para enseñar pruebas en el móvil; se sacó (o se iba a sacar) del proyecto común a `~/Desktop/pruebas-cloudflare/`. Se sube a mano, nunca automático.
- Este repo (glootie99/gorumon, rama claude/youthful-bell-o90t45) solo guarda copias de apoyo: logos, guía (`automatizacion/nodia/guia-claude-code.html`) y este resumen.

## Setup de Claude Code (ya montado)
- Skills: Impeccable (solo en el proyecto, hook compartido), frontend-slides y Ponytail (plugins compartidos en `.claude/settings.json`).
- OpenSpec (fuente única de specs, telemetría off) + Software Factory v1 de ZazenCodes adaptada: `/factory <change-id>` valida con OpenSpec, revisores según riesgo (bajo/medio/alto), sin merge automático (needs-human → `/factory approve`), agentes nunca hacen push ni despliegan. No usar `/opsx:apply`.
- Herramientas: Semgrep, Gitleaks, Trivy, Playwright. `scripts/instalar.sh` para nuevos socios.
- **Pendiente:** prueba en seco de la Factory (fase 4) antes de invitar a Alex y Toto al repo. Opción alternativa: Alex instala su propia Factory desde los repos públicos con el prompt de integración.

## Decisiones y conclusiones recientes
- Programa de escritorio de Numa: recomendada interfaz web en ventana propia (pywebview) con el código de Alex intacto detrás de una capa intermedia; Tauri si más adelante hace falta instalador/actualizaciones. Solo Mac (usa Apple Vision).
- Lectura sin IA: reglas genéricas + XML/QR Verifactu + mejora de la entrada (PDF por email, app de escaneo, rechazar fotos malas). Medir con datos del piloto antes de decidir IA.
- Contabilización (criterio de cada despacho): se puede sin IA con reglas como **datos** (proveedor+empresa → cuenta, palabras clave, sector), aprendiendo de las correcciones del asesor con alcance elegible. Producto único + configuración por despacho; mantenimiento solo para lo nuevo. Prueba de fuego: un segundo despacho sin código nuevo.
- Idea de facturas sintéticas con dificultad creciente + grupo ciego de facturas reales como juez: buena como segunda fase.
- Reparto actual: **Alex** hace la app lo más autónoma posible. **Adrián** investiga un servidor para que los clientes envíen facturas, con normas por cliente e IA detrás.
- Servidor: alquilado en la UE (no en casa), contratos RGPD (encargado/subencargados, EIPD), seguridad mínima (aislamiento por cliente, MFA, cifrado, copias 3-2-1, pentest). **No** usar el plan Max de Alex como motor del servidor (condiciones de uso, sin acuerdo de tratamiento, límites, menos seguro): API con condiciones comerciales o modelo local, y reglas sin IA para lo que se pueda.

## Reglas permanentes
- No inventar cifras, clientes ni testimonios. Datos de demo siempre ficticios.
- Nada se publica ni se fusiona sin aprobación humana.
