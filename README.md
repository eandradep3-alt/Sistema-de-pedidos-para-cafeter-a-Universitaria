# Caso 5: Sistema de Pedidos para Cafetería Universitaria

## 1. Descripción del Caso

El sistema es una aplicación web sencilla accesible desde computadoras o dispositivos móviles dentro del campus universitario. Está diseñada para agilizar el proceso de registro y gestión de pedidos de productos en la cafetería de la universidad. Su propósito es optimizar el proceso de toma, gestión y confirmación de pedidos, permitiendo a los estudiantes y al personal realizar solicitudes de manera rápida, confiable y organizada.

## 2.  Objetivo

- Automatizar el registro, confirmación y visualización de pedidos.
- Reducir tiempos de espera y errores en el proceso manual.
- Mejorar la eficiencia del servicio en la cafetería universitaria.
- Garantizar la seguridad y disponibilidad de la información de los pedidos.

## 3. Requerimientos funcionales

| **ID** | **Nombre del requisito** | **Descripción** | **Criterios de aceptación** |
| --- | --- | --- | --- |
| RF01 | Registro de pedidos | El sistema permitirá al usuario registrar un pedido seleccionando productos del menú, indicando la cantidad deseada y el nombre del cliente. | El sistema debe registrar el pedido y mostrar un mensaje de confirmación exitosa en menos de 3 segundos. |
| RF02 | Visualización del menú | El sistema mostrará al usuario todos los productos disponibles del menú, clasificados por categorías y precios. | El usuario debe poder visualizar el menú completo sin errores en menos de 2 segundos. |
| RF03 | Edición y cancelación de pedidos | El sistema permitirá modificar o cancelar pedidos antes de su confirmación final. | El sistema debe actualizar el pedido correctamente y mostrar mensaje de confirmación. |
| RF04 | Confirmación de pedidos | El sistema permitirá confirmar los pedidos registrados, generando un comprobante con los datos del cliente, hora y total. | El sistema debe generar y mostrar el comprobante en menos de 5 segundos. |
| RF05 | Historial de pedidos | El sistema permitirá consultar el historial de pedidos realizados, mostrando fecha, productos y cantidad total. | El usuario debe visualizar correctamente los pedidos anteriores con datos completos y sin errores. |

### 3.1 Requerimientos no funcionales

| **ID** | **Nombre del requisito** | **Descripción** | **Tipo** | **Criterios de aceptación** |
| --- | --- | --- | --- | --- |
| RNF01 | Rendimiento y capacidad bajo carga | El sistema deberá mantener un rendimiento estable procesando solicitudes simultáneas de hasta 30 usuarios concurrentes, sin superar un tiempo medio de respuesta de 3 segundos. | Requerimiento del producto (rendimiento). | 1. En pruebas de carga con 30 usuarios, el sistema no debe superar los 3 segundos de tiempo medio de respuesta.  2. El sistema no debe mostrar errores ni interrupciones durante el uso simultáneo. |
| RNF02 | Disponibilidad y recuperación ante fallos | El sistema deberá mantenerse operativo el 95% del tiempo, con capacidad de recuperación en menos de 1 minuto después de fallos menores. | Requerimiento de la organización (Fiabilidad / Disponibilidad). | 1. En simulaciones de fallos, el sistema se restablece en menos de 60 segundos. 2. En las pruebas de estabilidad, la disponibilidad no debe ser inferior al 95%. |
| RNF03 | Cumplimiento de estándares y normativas. | El sistema deberá cumplir con la Ley Orgánica de Protección de Datos Personales de Ecuador, aplicando cifrado AES-256 y control de accesos por credenciales únicas. | Requerimiento Externo (Legal / Ético) | 1. Auditorías de seguridad confirman cifrado de datos y contraseñas. 2. El sistema solicita consentimiento antes de almacenar datos personales. 3. Los usuarios no autenticados no pueden acceder a información del cliente. |

## 4. Tabla de pruebas

| **ID / Prueba** | **Tipo de pruebas** | **Requerimi entos asociados** | **Datos de entrada** | **Resultados esperados** | **Resultados obtenidos** |
|-----------------|----------------------|-------------------------------|------------------------|---------------------------|---------------------------|
| PU-01 | Unitarias | RF01-Registro de pedidos | Producto: "Café" Cantidad: 2 Cliente: "AnaTorres" | El sistema registra el pedido y muestra mensaje "Pedido registrado exitosamente "en un tiempo inferior a 3 segundos. | Pedido registrado correctamente. Tiempo de respuesta: 2.4 s |
| PU-02 | Unitarias | RF02-Visualización del menú | Solicitud de menú desde interfaz principal | El sistema muestra el menú completo con categorías y precios en menos de 2 segundos. | Menú cargado correctamente en 1.8 s |
| PU-03 | Unitarias | RF04 Confirmación de pedidos | Pedido ID #015 confirmado | El sistema genera y muestra comprobante con datos del cliente, hora y total en menos de 5 segundos. | Comprobante generado correctamente. Tiempo: 4.1 s |
| PV-01 | Validaciones | RF03 -Edición y cancelación de pedidos | Pedido ID #022 Acción: Cambiar cantidad de 1 a 3 unidades y luego cancelar el pedido | El sistema actualiza el pedido correctamente, muestra el mensaje "Pedido actualizado exitosamente" y permite cancelarlo sin errores | Pedido editado y cancelado correctamente. Mensajes mostrados según lo esperado. |
| PV-02 | Validaciones | RF05 - Historial de pedidos | Acción: Consultar historial de pedidos del cliente "Ana Torres" | El sistema muestra el historial con pedidos anteriores, incluyendo fecha, productos y cantidad total, sin errores. | Historial visualizado correctamente. Datos completos y ordenados cronológicamente. |

## 5. Tipos de mantenimientos propuestos

El sistema presentó dos situaciones problemáticas principales, y para cada una se aplicaron tres tipos de mantenimiento: correctivo, preventivo y perfectivo.

A continuación, se describe el análisis y las acciones aplicadas en cada caso.

### Situación 1: Registro incorrecto o lentitud al guardar pedidos

**Descripción del problema:**

El sistema presentaba lentitud y pérdida de información al registrar pedidos cuando varios usuarios interactuaban simultáneamente.

Esto se debía a la ausencia de control de concurrencia, validaciones insuficientes en cliente y servidor, y falta de mecanismos de recuperación ante desconexiones momentáneas.

**Mantenimientos aplicados:**

| **Tipos de mantenimientos** | **Descripción de la acción** |
| --- | --- |
| **Correctivo** | Se corrigieron errores de validación y fallos que causaban pérdida de datos en la base de datos. |
| **Preventivo** | Se implementaron pruebas de carga y monitoreo del sistema para anticipar fallos bajo alta concurrencia |
| **Perfectivo** | Se optimizaron consultas SQL, mejorando el tiempo de respuesta y la eficiencia general del sistema |

### Situación 2: Edición o cancelación incorrecta de pedidos confirmados

**Descripción del problema:**

El sistema permitía editar o cancelar pedidos que ya habían sido confirmados, generando inconsistencias en el estado de los pedidos y conflictos cuando varios usuarios intentaban modificar un pedido al mismo tiempo.

**Mantenimientos aplicados:**

| **Tipos de mantenimientos** | **Descripción de la acción** |
| --- | --- |
| **Correctivo** | Se corrigieron errores que permitían modificar o cancelar pedidos ya confirmados |
| **Preventivo** | Se implementó control de estados y concurrencia transaccional para evitar inconsistencias futuras |
| **Perfectivo** | Se mejoró la interfaz del sistema, añadiendo advertencias y validaciones visuales del estado de los pedidos. |

### 5.1 Cambio funcional propuesto

**Nombre:** Implementación de un Módulo de Control de Estados y Concurrencia (FSM) para la gestión segura de pedidos.

**Descripción del cambio:** Se integra una Máquina de Estados Finitos (FSM) que regule las transiciones válidas en el ciclo de vida de un pedido: (En selección → Confirmado → En preparación → Listo para recoger → Entregado).

Una vez que el pedido se encuentra en el estado **“Confirmado”**, las operaciones de edición o cancelación quedan bloqueadas para garantizar la integridad lógica y transaccional.

Además, se incluye:

- **Control de concurrencia optimista**, para evitar conflictos entre usuarios.
- **Módulo de auditoría**, que registra eventos críticos y mejora la trazabilidad.

## 6. Reflexión sobre la utilidad del Control de Versiones y Markdown

El **control de versiones** es una herramienta esencial en la ingeniería de software moderna, ya que permite gestionar los cambios realizados en el código y la documentación de forma estructurada, trazable y colaborativa. Entre sus principales beneficios se encuentra la posibilidad de mantener un flujo de trabajo seguro, registrar cada cambio en pequeños incrementos y revertir fácilmente cualquier error. Además, fomenta la experimentación sin riesgos, al permitir crear ramas o versiones paralelas para probar nuevas funcionalidades sin afectar la versión estable del proyecto.

Como señala Pressman (2010), los procesos de desarrollo ágil y colaborativo requieren prácticas que reduzcan el riesgo de errores y mejoren la comunicación entre los integrantes del equipo; en este contexto, el control de versiones actúa como un mecanismo de soporte indispensable. Según Sommerville (2011), el mantenimiento del software exige procesos sistemáticos que garanticen la continuidad operativa y la calidad del sistema a lo largo de su ciclo de vida. En ese sentido, el control de versiones se convierte en un pilar fundamental para mantener la integridad del proyecto, reducir riesgos y facilitar el trabajo en equipo de forma organizada.

Herramientas como Git y plataformas como GitHub materializan estos principios al registrar cada modificación mediante “commits descriptivos”, crear ramas para el desarrollo paralelo y restaurar versiones anteriores en caso de errores. Esto mejora la transparencia, fomenta la colaboración y fortalece la mantenibilidad del software.

De manera complementaria, el **lenguaje Markdown** ofrece una forma práctica y eficiente de documentar información técnica. Su sintaxis ligera mejora la claridad y accesibilidad de la documentación, permitiendo crear títulos, listas, tablas y enlaces sin depender de procesadores de texto complejos. Markdown promueve una escritura más directa y estandarizada. Al integrarse con sistemas de control de versiones como GitHub, permite que el código y la documentación evolucionen de forma coherente.

En conjunto, **Git/GitHub y Markdown** representan herramientas que fortalecen la calidad, sostenibilidad y trazabilidad de los proyectos de software. Ambas promueven la organización, la colaboración y la eficiencia, alineándose con los principios de mantenibilidad y gestión del cambio definidos por Sommerville (2011) y Pressman (2010). Su correcta aplicación no solo mejora la gestión técnica del sistema, sino también la experiencia y productividad de quienes lo desarrollan y documentan.

