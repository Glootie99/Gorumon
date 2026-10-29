# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Static single-file HTML/CSS/JS (user choice), stored in the repo and published as a claude.ai artifact for viewing and sharing.

## Users

Titulares y responsables de gestorías y asesorías fiscales/contables independientes (Madrid Norte primero, Barrio del Pilar). Cada trimestre reciben cajas, zips y emails de facturas de sus clientes y las graban a mano en su programa contable antes de presentar el 303 y el 111. Visitan la web después de una visita en persona o por recomendación, para entender qué es y decidir si piden un diagnóstico.

## Product Purpose

Sistema que lee las facturas que los clientes de la gestoría entregan, propone el asiento contable (tercero por NIF, IVA, retención, contrapartida) y lo presenta al asesor en Excel para revisión. Solo tras el visto bueno del asesor genera los ficheros de importación para su programa contable (hoy Sage). Cada corrección del asesor se convierte en una regla para el siguiente trimestre. Éxito: la gestoría recupera las horas de grabación y llega al cierre trimestral sin perseguir facturas.

## Positioning

- El asesor decide siempre: el sistema propone, nunca importa en la contabilidad por su cuenta.
- Aprende del criterio de ese despacho: cada corrección se vuelve regla con su prueba.
- Ningún importe se inventa ni se redondea: cuatro niveles de verificación (cuadres, está impreso, segunda lectura por otra vía, cola de revisión humana).
- Datos de los clientes en el equipo del despacho (local), no en una nube ajena.
- Gente del barrio que instala, adapta y responde; no un SaaS genérico.

## Operating Context

Ritmo trimestral (1T–4T, modelos 303 y 111). Entrada: zip o carpeta del cliente, PDFs, escaneos, fotos. Revisión en Excel (el idioma del asesor), a veces con correcciones dictadas en audio. Salida: XML/fichero de importación para el programa contable (Sage hoy; otros a preguntar: A3, Contasol). Plan General Contable: 6xx gastos, 7xx ingresos, 40/41 proveedores, 43 clientes, 472 IVA soportado, 4751 retenciones.

## Capabilities and Constraints

- Lectura en cascada: texto del PDF → OCR con dos motores → plantillas por proveedor → modelo de IA solo para lo que queda.
- Lee facturas recibidas; no emite facturas (emitir entraría en Verifactu).
- Modelo comercial: alta + cuota mensual de mantenimiento. Precios NO se publican en la web (a validar).
- Nombre comercial: provisional «Asiento» (inventado por Claude, a confirmar por el usuario).
- Contacto real (email/teléfono): pendiente; la web usa un formulario de muestra.

## Brand Commitments

Idioma principal español; la web debe ofrecer también inglés. Tono cercano y directo, de alguien del oficio.

## Evidence on Hand

Un piloto real en una gestoría (no nombrarla sin permiso escrito). No hay testimonios, cifras medidas de ahorro, logos de clientes ni precios validados: no fabricarlos. Se puede mostrar el proceso y una calculadora con los números que introduce el visitante, y datos de ejemplo marcados como ficticios.

## Product Principles

1. El criterio del asesor manda; la máquina prepara.
2. Mostrar el proceso en vez de prometer cifras.
3. Nada pasa en silencio: lo dudoso se marca, no se disimula.
4. Encaja en lo que el despacho ya usa (Excel, su programa contable).
