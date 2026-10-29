# Proyecto automatización — Madrid Norte

Consultora de automatización a medida para negocios locales independientes de Madrid Norte (empezando por el Barrio del Pilar), vendida en persona. Punto de partida: el sistema de facturas ya funcionando en una gestoría piloto.

Traído a Claude Code el 29-10-2026 desde los chats y artefactos de claude.ai.

## Contenido

| Ruta | Qué es |
| --- | --- |
| [`docs/plan-el-pilar.md`](docs/plan-el-pilar.md) | Plan de negocio: DAFO, diferenciación, clientes objetivo, 4 módulos, precios, guion de visita, próximos pasos |
| [`docs/maquetas-demo.md`](docs/maquetas-demo.md) | Las tres maquetas de demo (gestoría, clínica, academia): pantallas, datos, guion de 10 min, precios, checklist |
| [`datos/candidatos_madrid_norte.csv`](datos/candidatos_madrid_norte.csv) | Registro de 170 negocios candidatos (también en `.json`) |
| [`referencia/sistema-facturas-por-dentro.html`](referencia/sistema-facturas-por-dentro.html) | Cómo está montado el sistema de facturas de la gestoría piloto (módulo 1) |
| [`referencia/proyecto-automatizacion-hub.html`](referencia/proyecto-automatizacion-hub.html) | Copia del panel "Proyecto automatización" (abre en el navegador) |

### Registro de candidatos

Columnas: `sector, subsector, nombre, direccion, distrito, barrio, telefono, prioridad, maqueta, nota, estado`.
Datos de Google Maps del 29-10-2026: confirmar teléfono y horario antes de ir.

- **Sectores:** Clínicas 68 · Academias 40 · Gestorías 27 · Talleres 19 · Fincas 16
- **Prioridad:** Alta 126 · Media 34 · Baja 10
- **Distritos:** Fuencarral-El Pardo 73 · Hortaleza 39 · Tetuán 31 · Chamartín 27
- **Estado:** todos "Pendiente" (0 visitados)

## Originales en claude.ai

Artefactos:
- Proyecto automatización (panel): https://claude.ai/artifact/SeAeXM8ZDsiB4hbzMkrPLe
- Automatizaciones para negocios locales — El Pilar: https://claude.ai/artifact/HESCfoLKYtWybjbqzbHjTH
- Tres maquetas de demo: https://claude.ai/artifact/BMYAn4nBzPYMf3fychCTim
- SistemaFacturas por dentro: https://claude.ai/artifact/GZwmmRMputqM9gBJ3vAsqT

Conversaciones:
- Proyecto de software para gestorías (valoración y "empleado digital"): https://claude.ai/chat/881e1e66-0eaa-4d83-9065-336be92dacc1
- Verifactu y normativa legal: https://claude.ai/chat/477b88a5-ba51-4e2c-a544-636fd967bdcb
- Maquetas y candidatos Madrid norte: https://claude.ai/chat/9948da7d-4446-44c3-834d-58fa966f9213
- Vestimenta adecuada (visitas puerta a puerta): https://claude.ai/chat/7bcb9992-c9c2-4fd2-b1ed-a55584a46c19
