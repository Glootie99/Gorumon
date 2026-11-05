# Encargo: montar Numa Evo (web nueva de Numa con OpenSpec + Software Factory)

> **Cómo usarlo.** Adrián abre Claude Code en `~/Desktop/automatization` y dice:
> «lee y ejecuta `~/Desktop/gorumon-informe/automatizacion/numa-evo/ARRANQUE-NUMA-EVO.md`».
> Escrito el 05-11-2026 en el chat de la nube con Adrián. Todo se hace **en local, en el Mac de Adrián**.

---

## 0. Reglas de este encargo (no se rompen)

1. **Solo Numa para gestorías.** Nada de Nodia, clínicas, academias ni otros sectores.
2. **La web actual no se toca.** Se **duplica** y solo se trabaja sobre la copia, dentro de `~/Desktop/automatization/Numa Evo/`.
3. **Todo en local.** Numa Evo **no sube a GitHub** por ahora: ni repo nuevo ni push. Ojo: la carpeta está dentro del repo `automatization`, que sí tiene remoto. Antes de nada, añade `Numa Evo/` al `.gitignore` de `automatization` y comprueba con `git status` que no aparece. Numa Evo lleva su propio `git init` local, sin remoto.
4. **Adrián está aprendiendo la Factory.** En **cada paso**, dile qué comando escribir, qué hace y qué esperar. Nunca lances un comando de la Factory sin explicarlo antes. Al final de cada respuesta, propón **el siguiente comando**.
5. **OpenSpec y la Factory, siempre.** Cada cambio de la web es un cambio de OpenSpec (`openspec/changes/<id>/`) construido con `/factory <id>`. **Nunca `/opsx:apply`.** Nada se fusiona ni se publica sin el «sí» de Adrián (`/factory approve`). Los agentes nunca hacen push ni despliegan.
6. **Ningún dato real.** Ni de clientes del padre de Alex ni de ninguna gestoría. Los ejemplos de la web y las demos van con datos inventados (empresas `zzz…`). No inventes cifras, clientes ni testimonios.
7. **Pregunta antes de hacer algo irreversible** (borrar, sobrescribir o mover ficheros fuera de `Numa Evo/`).

---

## 1. El contexto de Numa (resumen; las fuentes están en el §4)

**Quiénes.** Alex (hermano de Adrián) construyó con Claude Code un sistema de facturas para el despacho de asesoría de su padre. Adrián lleva el servidor, la venta, el marketing y la web. Son hermanos: no se habla de pactos de socios ni de NDA entre ellos.

**Qué hace el software de Alex.** Recibe las facturas del trimestre de un cliente de la gestoría (PDF, escaneo o foto). Las lee en cascada: texto del PDF, OCR, plantillas y, solo al final, IA. Propone el tercero, la cuenta y la contrapartida. Saca un **Excel** para que el asesor revise y, solo tras su «sí», un **XML** que la gestoría importa en Sage. Siempre revisa una persona. Hoy aprende las reglas con Claude Code y Alex delante; Alex está haciendo que aprenda solo de las correcciones.

**Cifras que se pueden enseñar (siempre con su muestra):**
- Cuenta del proveedor: 140 aciertos de 168 propuestas (83 %), proponiendo en el 42 % de los casos.
- Lo que corrige el asesor no se repite (51/51, 38/38).
- De 30 a 45 minutos por cliente y trimestre; unas 2 horas uno difícil.
- No hay todavía cifra de cuánto tardaba el padre antes.

**Qué vende Numa ahora: el servicio personalizado.** No es un programa enlatado. «**Nos sentamos con vuestra gestoría, aprendemos cómo trabajáis y montamos el sistema con vuestro criterio.** Os devolvemos cada trimestre las facturas leídas y contabilizadas; vosotros solo revisáis lo dudoso.» Cebo: **piloto gratis con un cliente suyo**. Se habla de **horas y del cierre del trimestre**, no de IA. Marca: «Numa aprende contigo», un «mini Numa» por gestoría. Planes de ejemplo: Numa Lector · Numa aprende contigo · El segundo tú (ancla cara). Precios **sin cerrar**: no poner cifras en la web.

**Primeros clientes:** visitas en persona a la **gestoría Toro** y a la del **padre de Alfredo** (semana del 10-11-2026). En los pilotos los datos van por Google Drive con contrato de encargo; el servidor llega después.

**Servidor decidido (para lo que diga la web sobre datos y seguridad):** VPS Hetzner en Alemania (UE), IA procesada en la UE (Bedrock perfil UE o Mistral), cifrado, doble factor, copias en otro proveedor de la UE, pentest antes del primer cliente real y contrato de encargo (art. 28 RGPD) con cada gestoría. **No prometer «datos en vuestra oficina»**: decir por escrito dónde está cada dato.

**Competencia (para el mensaje de la web):** leer facturas y proponer el asiento ya lo venden Inmatic, Copilot Gestoría (0-99 €/mes), Contabilify, Dijit, Holded para asesorías, Esphera.ai… AutoApunte ya vende servicio a medida para asesorías. **Nuestro hueco, por demostrar:** aprender el **criterio de cada gestoría** (no solo por proveedor), arrancar con **su histórico de Sage**, **sentarnos con ellos** y **trabajar con su Sage/A3 sin cambiar de programa**. No nombrar competidores en la web ni decir que no hacen algo que no hemos probado.

---

## 2. Lo que tienes que hacer, en orden

### Paso 1: entender lo que hay (solo leer)
1. Lee `CLAUDE.md`, `AGENTS.md` y `ESTADO.md` de `~/Desktop/automatization`.
2. Localiza **la web actual de Numa** (la que Adrián considera «genial»). Busca en `~/Desktop/automatization` (carpeta `numa/`, `deploys/` u otra) y en `~/Desktop` (también `~/Desktop/pruebas-cloudflare/`). **No es la web de Nodia** (`~/Desktop/nodia`).
3. ⛔ **Enséñale a Adrián qué has encontrado** (ruta, qué tecnología usa, cuántos ficheros) y **espera su confirmación** de que es esa antes de copiar nada.

### Paso 2: la carpeta limpia
1. Añade `Numa Evo/` al `.gitignore` de `automatization` y comprueba con `git status` que no aparece.
2. Dentro de `~/Desktop/automatization/Numa Evo/`: `git init` (sin remoto).
3. Copia la web confirmada a `Numa Evo/web/`. **Copia, no muevas.** Comprueba que el original sigue igual (mismo número de ficheros).
4. Copia la configuración de trabajo desde `~/Desktop/automatization`: `openspec/` (sin los cambios de otros proyectos), `factory/`, los agentes, skills y hooks de `.claude/` que usa la Factory, y `AGENTS.md`. Mantén la telemetría de OpenSpec apagada.
5. Comprueba que funciona: `openspec validate` (o el comando equivalente que use el proyecto) y que la Factory responde. Si algo falla, explícaselo a Adrián en lenguaje sencillo.
6. Comprueba que la web copiada arranca en local (`npm install` + `npm run dev`, o lo que corresponda) y dile la dirección para abrirla en el navegador.

### Paso 3: el contexto para cualquier chat nuevo
Crea en `Numa Evo/`:
- `CLAUDE.md`: las reglas del §0 de este encargo, en corto, y que lea `docs/CONTEXTO-NUMA.md` al empezar.
- `docs/CONTEXTO-NUMA.md`: el §1 de este encargo, ampliado con las fuentes del §4 (sin datos reales).
- `docs/informes/`: copia de `INVESTIGACION-SERVIDOR.md` y `COMPETENCIA-NUMA.md` (del repo `~/Desktop/gorumon-informe/automatizacion/`).
- `docs/GUIA-FACTORY.md`: chuleta para Adrián, en español sencillo. Qué es un cambio de OpenSpec, el ciclo completo con los comandos exactos de este proyecto (proponer → revisar → `/factory <id>` → mirar el resultado → `/factory approve` o pedir cambios), qué hace cada nivel de riesgo, qué hacer si la Factory se para en «needs-human», y qué no usar nunca (`/opsx:apply`).
- Primer commit local: «Numa Evo: arranque».

### Paso 4: la primera clase práctica (con Adrián, paso a paso)
Primer cambio de OpenSpec: **«web-servicio-personalizado»**. Rediseñar la copia de la web para vender el servicio personalizado a gestorías:
- Cabecera: el cierre del trimestre resuelto, con vuestro criterio.
- Cómo funciona: nos sentamos · aprendemos vuestras normas · leemos y contabilizamos · revisáis lo dudoso · lo importáis en vuestro Sage/A3.
- El piloto gratis con un cliente vuestro.
- Seguridad y datos: UE, contrato de encargo, revisión humana siempre.
- Contacto para pedir la visita.
- Sin precios, sin testimonios inventados y sin nombrar competidores.

Hazlo **con Adrián**, explicando cada comando antes de lanzarlo:
1. Escribid juntos la propuesta del cambio. Que Adrián la lea y diga «sí» o qué cambiar.
2. Valídala con OpenSpec.
3. Constrúyela con `/factory web-servicio-personalizado`.
4. Que Adrián la vea en el navegador.
5. Si le gusta, `/factory approve`; si no, ajustar la propuesta y repetir.

---

## 3. Lo que entregas al final de cada sesión
Un mensaje corto con: qué se hizo, dónde está (rutas), cómo verlo y **el siguiente comando recomendado**. Si la sesión se corta, deja el estado en `Numa Evo/ESTADO.md`.

## 4. Fuentes de contexto (léelas para ampliar el §1, sin copiar datos reales)
- `~/Desktop/gorumon-informe/automatizacion/servidor/INVESTIGACION-SERVIDOR.md`
- `~/Desktop/gorumon-informe/automatizacion/competencia/COMPETENCIA-NUMA.md`
- Google Drive, carpeta «Factucoin - documentos 04-11-2026» (de Alex): `PARA-IA/0-CONTEXTO-COMUN.md`, `FOCO.md`, `HOJA-DE-RUTA.md`, `VENTA-EN-PERSONA.md`, `PARA-LEER/4B-ADRI-VENTA-MARKETING-NUMEROS.md`.
- Google Drive, carpeta «Tareas Adri»: los resúmenes del servidor y de la competencia.
- Las marcas de Numa: `automatizacion/assets/marca/` del repo Gorumon (logo NUMA con la N de cuenta en T).
