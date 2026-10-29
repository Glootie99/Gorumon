# Contexto para Claude Code — Proyecto automatización

Proyecto de Adrián (perfil ciberseguridad/OT) con un amigo desarrollador (Alex, autor del sistema de facturas de la gestoría piloto). Objetivo: vender automatización a medida a pymes de Madrid Norte y conseguir los primeros clientes.

## Decisiones ya tomadas (no re-litigar sin motivo)
- Sectores iniciales, en este orden: gestorías → clínicas → academias. Evitar hostelería, moda, franquicias y La Vaguada.
- Posicionamiento: "empleado digital" que conecta lo que el negocio ya usa; no competir con SaaS de ~25 €/mes en recordatorios/OCR.
- Software local, datos en el negocio. Capa común obligatoria: copias, acceso remoto seguro, permisos, registro de cambios, documentación.
- 4 módulos base: (1) facturación y documentos — hecho; (2) citas y recordatorios; (3) cobros recurrentes; (4) panel de control.
- Venta: visita → propuesta escrita en 2–3 días → prueba rápida → proyecto con presupuesto aceptado. Nunca semanas de desarrollo gratis.
- Maquetas: genéricas por sector, datos 100 % ficticios, offline, máx. 1–2 semanas cada una.

## Restricciones legales a tener presentes
- Emitir facturas = sistema de facturación sujeto a Verifactu (posible aplazamiento a 2028 pendiente de BOE; verificar fecha vigente).
- Clínicas: datos de salud (RGPD categoría especial); recordatorios sin revelar tratamiento; WhatsApp solo por API oficial de Business.
- Academias: datos de menores (consentimiento de tutores), órdenes SEPA firmadas.
- Nunca usar datos reales de la gestoría piloto en demos sin permiso escrito.

## Archivos
- `docs/` plan de negocio y maquetas (Markdown, fuente de verdad aquí).
- `datos/candidatos_madrid_norte.csv|json` registro de 170 candidatos; actualizar la columna `estado` al visitar.
- `referencia/` copias HTML de los artefactos originales (solo lectura).
- Idioma de trabajo: español.
