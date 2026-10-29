# Tres maquetas de demo: gestoría, clínica y academia

## Enfoque común

Cada maqueta es una demo funcional de 10 minutos, con datos ficticios del sector, que corre en el portátil sin internet y enseña un antes/después con una cifra de ahorro. No es el producto final: es lo que convierte una visita en un diagnóstico.

Las tres salen de los mismos 4 módulos base; cambia qué módulo es la estrella y cómo se llama cada cosa en la pantalla.

| Módulo | Gestoría | Clínica | Academia |
| --- | --- | --- | --- |
| Facturación y documentos | **Estrella** | Secundario (mutuas, bonos) | Secundario (recibos) |
| Citas y recordatorios | Secundario (avisos de cierre trimestral) | **Estrella** | Secundario (avisos a familias) |
| Cobros recurrentes | No | Secundario (bonos) | **Estrella** |
| Panel de control | Sí | Sí | Sí |

**Reglas para las tres demos**

- **Datos 100 % ficticios pero creíbles.** Nunca datos de la gestoría piloto sin su permiso por escrito: enseñar datos de un cliente a otro hunde la confianza y es un problema de RGPD.
- **Funciona en local y offline.** La venta es en el local del cliente; no dependas del wifi del negocio.
- **Una sola cifra protagonista** por maqueta (horas, euros perdidos, euros pendientes). Se calcula en vivo con los datos que el dueño te diga.
- **Tres pantallas como máximo en la demo.** El resto existe por si preguntan.
- **Cierre siempre igual:** “con tus datos reales esto lo medimos en un diagnóstico de una hora”.

**Ojo legal con el módulo de facturación:** si vuestro software *emite* facturas (no solo las lee), pasa a ser un sistema informático de facturación y debe cumplir Verifactu. La obligación llega el 1 de enero de 2027 para sociedades y el 1 de julio de 2027 para autónomos ([Real Decreto-ley 15/2025](https://www.conversoriaecnae.es/guia/verifactu/plazos-2027)). Leer facturas recibidas y exportarlas no entra; emitirlas, sí.

### Cómo diferenciarnos

Recordatorios, OCR de facturas y recibos ya los dan AgendaPro, Fisiopublic, Acadesoft, Holded o Dext por unos 25 €/mes. No competimos ahí: la maqueta es una capa por encima de lo que ya usan, un "empleado digital".

- **Conecta** su agenda, banco, email, programa contable y gestoría sin cambiarles nada.
- **Entiende lo desordenado:** audios, fotos de tickets, emails con PDFs, Excel caóticos.
- **Conversa:** resuelve por WhatsApp cambios de cita o dudas con datos reales.
- **Actúa solo:** reactiva clientes inactivos, persigue impagos, avisa de huecos libres.
- **Resume:** mensaje al dueño cada lunes con lo importante.

**Momento "wow" en cada demo (que pase algo delante del dueño):**

| Maqueta | Qué se hace en vivo |
| --- | --- |
| Gestoría | Foto a un ticket real y aparece clasificado en 10 s; un email con 5 facturas mezcladas, todas procesadas |
| Clínica | El dueño escribe desde su móvil "quiero cita mañana" y recibe huecos reales al momento |
| Academia | El sistema redacta y programa avisos de impago personalizados según lo que deba cada uno |

**Argumentos:** funciona con lo que ya tienen, datos en local y alguien del barrio detrás. Ya hay productos que se anuncian como "empleado digital" (p. ej. en fisioterapia), así que la ventaja no es la idea, es la integración a medida. Precio: se compara con media jornada de un empleado, no con un SaaS de 25 €.

## Maqueta 1 — Gestoría: “La bandeja de facturas que se vacía sola”

Es la maqueta más rápida de montar porque ya tenéis el caso hecho: se trata de empaquetarlo con datos ficticios y una pantalla de resultados.

**Dolor que ataca:** picar facturas de clientes a mano, perseguir a los clientes que no mandan facturas antes del cierre trimestral y errores de NIF o IVA que se descubren tarde.

**Pantallas**

1. **Bandeja de entrada.** Una carpeta o un correo donde caen las facturas de todos los clientes. Lista con estado por factura: leída, a revisar, exportada.
2. **Ficha de factura.** PDF a la izquierda; a la derecha, los campos extraídos (emisor, NIF, fecha, base, tipo y cuota de IVA, retención, total). Alertas en rojo: NIF no válido, base × IVA no cuadra, factura duplicada.
3. **Exportación contable.** Un botón genera el fichero de importación para su programa (preguntad cuál usan: A3, Contasol, Sage...).
4. **Panel por cliente.** Facturas recibidas este trimestre y clientes a los que les faltan. Botón “enviar recordatorio” con texto tipo “te faltan las facturas de septiembre”.
5. **Panel de la gestoría.** Facturas procesadas en el mes y horas ahorradas estimadas.

**Datos de la demo**

- 3 clientes ficticios: un fontanero autónomo, un bar y una clínica dental.
- 60 facturas PDF variadas, con trampas a propósito: una escaneada torcida, una duplicada, una con el IVA mal calculado y una de un proveedor con NIF inválido.

**Guion de 10 minutos**

1. Pregunta de entrada: “¿Cuántas facturas picas al trimestre y cuánto tardas en cada una?”. Apunta las dos cifras.
2. Arrastra las 60 facturas a la bandeja. Mientras procesa, cuenta el caso de la gestoría piloto (con sus cifras reales medidas).
3. Abre la factura con IVA mal calculado: “esto lo habrías visto en el cierre”.
4. Exporta y enseña el fichero listo para importar.
5. Panel por cliente: “estos dos te deben facturas; el recordatorio sale solo el día que digas”.
6. Calcula en voz alta con sus cifras: facturas al trimestre × minutos por factura = horas que recuperan.
7. Cierre: diagnóstico de una hora con sus facturas reales.

**Gancho de calendario:** Verifactu obliga a sociedades el 1 de enero de 2027 y a autónomos el 1 de julio de 2027. Las gestorías van a tener a todos sus clientes preguntando en los próximos meses; vosotros no vendéis Verifactu, vendéis tiempo libre para atender esa avalancha.

**Precio orientativo (propuesta, a validar con el primer cliente):** alta de 600 a 1.200 € según el programa contable, y cuota de mantenimiento de 100 a 150 €/mes.

**Pregunta abierta para tu amigo:** ¿qué tasa de acierto tiene la extracción con facturas escaneadas y en papel? Es lo primero que preguntará una gestoría.

## Maqueta 2 — Clínica: “La agenda sin huecos”

Pensada para fisioterapia, que es el caso más claro; con cambiar nombres sirve para podología, psicología, nutrición y pequeñas dentales. La cifra protagonista son los euros perdidos por citas a las que nadie viene.

**Dolor que ataca:** pacientes que no aparecen, llamadas para recordar citas, huecos que no se rellenan, bonos de sesiones apuntados en papel y facturas a mutuas.

**Pantallas**

1. **Agenda semanal** por profesional, con colores: confirmada, pendiente, cancelada.
2. **Recordatorio automático** 24 h antes por WhatsApp o SMS, con botones “confirmo” y “no puedo ir”. En la demo se enseña el móvil recibiéndolo.
3. **Lista de espera.** Cuando alguien cancela, se avisa al siguiente de la lista y el hueco se rellena solo.
4. **Bonos de sesiones.** Ficha del paciente con “bono de 10: quedan 3” y aviso cuando se acaba.
5. **Panel.** Ausencias del mes, huecos rellenados y euros recuperados.

**Datos de la demo**

- Clínica ficticia con 3 fisios y unas 120 citas a la semana.
- 8 pacientes con bono, 3 cancelaciones en la semana y 2 personas en lista de espera.
- Tu propio móvil dado de alta como paciente, para que el recordatorio llegue en directo.

**Guion de 10 minutos**

1. Pregunta de entrada: “¿Cuántos pacientes te fallan a la semana y cuánto cobras la sesión?”. Apunta las dos cifras.
2. Agenda: crea una cita para mañana con tu móvil. Lanza el recordatorio y enséñale el WhatsApp llegando.
3. Pulsa “no puedo ir” desde el móvil: el hueco se libera y la lista de espera recibe el aviso.
4. Ficha de bono: “esto hoy lo llevas en una libreta”.
5. Calcula en voz alta: fallos a la semana × precio × 4 = euros al mes que se pierden.
6. Cierre: diagnóstico de una hora con su agenda real.

**Lo delicado (aquí tu perfil de ciberseguridad vende):** son datos de salud, categoría especial en el RGPD. Hace falta contrato de encargado del tratamiento, cifrado, control de accesos y copias. El texto del recordatorio no debe revelar el tratamiento, solo día y hora. Y el envío por WhatsApp necesita la API oficial de WhatsApp Business y el consentimiento del paciente; las apps no oficiales pueden acabar con el número bloqueado.

**Precio orientativo (propuesta):** alta de 400 a 800 € y cuota de 60 a 120 €/mes, más el coste de los mensajes si se envían por SMS o WhatsApp.

**Pregunta abierta para tu amigo:** ¿se integra con la agenda que ya usan (muchas clínicas tienen un programa de gestión) o la sustituye? Sustituir es mucho más difícil de vender.

## Maqueta 3 — Academia: “Las cuotas que se cobran solas”

Pensada para academias de idiomas o de refuerzo; adaptable a autoescuelas, escuelas de música y escuelas infantiles. La cifra protagonista es el dinero pendiente de cobro hoy.

**Dolor que ataca:** cobrar cuotas mes a mes, perseguir impagos con incomodidad, avisar a familias de cambios y llevar matrículas y asistencia en hojas sueltas.

**Pantallas**

1. **Alumnos y grupos.** Cada alumno con su grupo, horario, cuota y forma de pago.
2. **Remesa mensual.** Un botón genera los recibos del mes: fichero de domiciliación para el banco o enlace de pago para quien paga con tarjeta o Bizum.
3. **Impagos.** Lista de quien debe, con avisos escalonados automáticos (amable el día 1, recordatorio el 5, aviso firme el 10). El dueño deja de ser el que reclama.
4. **Comunicación con familias.** Aviso a un grupo entero: “el jueves no hay clase”.
5. **Panel.** Cobrado este mes, pendiente, alumnos activos y bajas.

**Datos de la demo**

- Academia de inglés ficticia con 90 alumnos en 12 grupos.
- 7 impagos repartidos en distintos estados de aviso.
- Tu móvil como “madre de un alumno” para recibir el aviso en directo.

**Guion de 10 minutos**

1. Pregunta de entrada: “¿Cuántos alumnos tienes, cuánto es la cuota y cuántos se retrasan cada mes?”.
2. Genera la remesa del mes con un clic.
3. Abre impagos: “estos 7 recibirán el aviso solos; tú no tienes que llamar a nadie”.
4. Manda el aviso de clase cancelada y enséñalo llegando a tu móvil.
5. Panel: pendiente de cobro en euros.
6. Cierre: diagnóstico de una hora con su listado real de alumnos.

**Lo delicado:** muchos alumnos son menores, así que los datos y los mensajes van a padres o tutores, con su consentimiento. La domiciliación bancaria exige una orden SEPA firmada por cada familia; la maqueta debe enseñar dónde se guarda.

**Precio orientativo (propuesta):** alta de 400 a 700 € y cuota de 50 a 100 €/mes.

**Pregunta abierta para tu amigo:** ¿generamos el fichero de remesa estándar para que lo suba el banco, o integramos una pasarela de pago? Lo primero es más sencillo y suficiente para empezar.

## Comparativa y orden de construcción

Construid en este orden: gestoría, clínica, academia. Cada maqueta reutiliza piezas de la anterior y la gestoría os abre contactos para las otras dos.

|  | Gestoría | Clínica | Academia |
| --- | --- | --- | --- |
| Frase gancho | “Tu bandeja de facturas se vacía sola” | “Cada paciente que no viene te cuesta una sesión” | “Deja de perseguir cuotas” |
| Cifra protagonista | Horas al trimestre | € perdidos al mes | € pendientes hoy |
| Módulo estrella | Facturación y documentos | Citas y recordatorios | Cobros recurrentes |
| Esfuerzo de montaje | Bajo: ya existe | Medio: mensajería | Medio: remesas |
| Riesgo legal principal | Verifactu si emite facturas | Datos de salud | Datos de menores, SEPA |
| Alta orientativa | 600–1.200 € | 400–800 € | 400–700 € |
| Cuota orientativa | 100–150 €/mes | 60–120 €/mes | 50–100 €/mes |

1. **Gestoría primero.** Empaquetar el caso real con datos ficticios y medir las cifras del piloto.
2. **Clínica después.** Reutiliza el panel y añade agenda y mensajería; la mensajería servirá también para la academia.
3. **Academia al final.** Reutiliza mensajería y panel; solo añade alumnos, remesas e impagos.

Los precios son una propuesta de partida, no un dato de mercado: ajustadlos tras los tres primeros diagnósticos.

## Checklist antes de salir a la calle

- [ ] Cifras reales medidas en la gestoría piloto (horas antes y después, facturas al mes)
- [ ] Permiso por escrito de la gestoría piloto para usarla como referencia
- [ ] Las tres maquetas funcionando offline en un portátil, con datos ficticios cargados
- [ ] Móvil de demo dado de alta para recibir recordatorios y avisos en directo
- [ ] Hoja de diagnóstico de una hora impresa (preguntas y cálculo de ahorro)
- [ ] Modelo de contrato de encargado del tratamiento listo
- [ ] Decidido quién hace el mantenimiento y cómo (remoto o visita)
- [ ] Tarjeta o una hoja con contacto, para dejar en los locales donde el dueño no esté
- [ ] Registro de candidatos impreso o en el móvil para apuntar visitas
