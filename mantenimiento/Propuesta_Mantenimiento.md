# Propuesta de Mantenimiento – Sistema de Pedidos para Cafetería Universitaria

## 1. Descripción General del Sistema
El sistema es una aplicación web accesible desde computadoras o dispositivos móviles dentro del campus universitario, diseñada para agilizar el proceso de registro y gestión de pedidos de productos en la cafetería. Su propósito es optimizar el tiempo de atención y mejorar la experiencia del usuario mediante un flujo automatizado de pedidos.

## 2. Análisis del Problema y Enfoque de Mantenimiento

El sistema actual presenta limitaciones en la validación de entradas, manejo de concurrencia y control de estados de los pedidos, lo que afecta la confiabilidad y mantenibilidad del software.  
Por ello, se propone aplicar acciones de **mantenimiento correctivo, preventivo y perfectivo**, fundamentadas en Sommerville (2011) y Pressman (2010), orientadas a fortalecer la estabilidad y calidad del producto.

A continuación, se describen las dos principales situaciones problemáticas identificadas en el sistema y las acciones de mantenimiento aplicadas para su corrección y mejora.

## 2.1 Situación 1: Registro incorrecto o fallas al guardar pedidos

### Descripción del problema
El sistema presenta lentitud o pérdida de información al registrar pedidos cuando múltiples usuarios interactúan simultáneamente, debido a la ausencia de control de concurrencia y validación de las transacciones.
Además, permite el ingreso de datos inválidos (por ejemplo, texto en campos numéricos o cantidades negativas) por falta de validaciones en cliente y servidor.  
Ante desconexiones momentáneas, no existe un mecanismo de reintento o persistencia transaccional, lo que ocasiona pérdida de pedidos y afecta la fiabilidad del servicio.

### Causas técnicas
- Falta de validaciones en la capa cliente/servidor.  
- Mala optimización de consultas SQL.  
- Ausencia de mecanismos de recuperación o reintento.

### Impacto
- Pedidos duplicados o no guardados.  
- Experiencia de usuario negativa y pérdida de confianza.  
- Cobros incorrectos y pérdida de información relevante.

### Mantenimientos aplicados

| **Tipo de mantenimiento** | **Descripción de la acción** |
|----------------------------|-------------------------------|
| **Correctivo** | Se deben corregir errores de validación y fallos que causan pérdida de datos. |
| **Preventivo** | Implementar pruebas de carga y monitoreo para prevenir fallos futuros. |
| **Perfectivo** | Optimizar consultas SQL, mejorar el tiempo de respuesta y aumentar la eficiencia del sistema. |

---


## 2.2 Situación Problemática 2: Edición o cancelación incorrecta de pedidos confirmados

### Descripción del problema
El sistema permite editar o cancelar pedidos que ya fueron confirmados, generando inconsistencias entre el estado lógico del pedido y la información almacenada en la base de datos.  
Si dos usuarios intentan modificar el mismo pedido simultáneamente, pueden producirse conflictos debido a la ausencia de control de concurrencia transaccional.

### Causas técnicas
- Falta de control de estados en la lógica de negocio.  
- Ausencia de control de concurrencia y auditoría.  
- No existen límites temporales para la cancelación de pedidos.

### Impacto
- Pedidos preparados erróneamente o cancelados tarde.  
- Pérdida de fiabilidad del sistema y posibles pérdidas económicas.  
- Confusión del personal al gestionar pedidos.

### Mantenimientos aplicados

| **Tipo de mantenimiento** | **Descripción de la acción** |
|----------------------------|-------------------------------|
| **Correctivo** | Corregir errores que permiten modificar pedidos confirmados. |
| **Preventivo** | Implementar control de estados y concurrencia para evitar inconsistencias futuras. |
| **Perfectivo** | Mejorar la interfaz con advertencias y validación visual del estado del pedido. |


---

## 3. Cambio funcional propuesto

### Nombre del cambio

Implementación de un Módulo de Control de Estados y Concurrencia (FSM) para la gestión segura de pedidos.

### Descripción
El cambio funcional consiste en incorporar una **Máquina de Estados Finitos (FSM)** que regule las transiciones válidas dentro del ciclo de vida de los pedidos:  
**(En selección → Confirmado → En preparación → Listo para recoger → Entregado).**

Una vez que el pedido se encuentra en el estado **"Confirmado"**, las operaciones de edición o cancelación quedan bloqueadas, garantizando la integridad lógica y transaccional del sistema.  

Además, se implementarán los siguientes componentes:
- **Control de concurrencia optimista**, para evitar conflictos entre usuarios.
- **Módulo de auditoría**, que registra eventos críticos y mejora la trazabilidad.

### Beneficios
- Corrige fallas lógicas en la validación de estados y manipulación de datos.  
- Previene errores de concurrencia mediante control de estados.  
- Mejora la usabilidad y transparencia con advertencias visuales.  
- Aumenta la trazabilidad, estabilidad y mantenibilidad del sistema.

### Implementación Técnica

1. **Diseño:** modelado UML de la FSM, y definición de reglas de transición.  
2. **Desarrollo:** refactorización de consultas SQL y desarrollo del módulo FSM.  
3. **Pruebas:** ejecución de pruebas unitarias, de carga, de regresión y de concurrencia.  
4. **Despliegue:** liberación progresiva y monitoreo post-implementación.


### Impacto en la Mantenibilidad y Calidad
- Reducción del tiempo medio de resolución de fallos (MTTR).  
- Mejora de la integridad y consistencia de los datos.  
- Mayor modularidad del código y facilidad para futuras extensiones.  
- Incremento en la confiabilidad, rendimiento y trazabilidad del sistema.

## 4. Conclusión

La implementación de un enfoque de mantenimiento proactivo que integra acciones **correctivas, preventivas y perfectivas** resulta esencial para garantizar la sostenibilidad y evolución del **Sistema de Pedidos para Cafetería Universitaria**.  
La incorporación del **Módulo de Control de Estados y Concurrencia (FSM)** no solo corrige las fallas existentes en la integridad y consistencia de los datos, sino que también mejora la **modularidad, trazabilidad y mantenibilidad** del software, fortaleciendo su estructura interna para futuras ampliaciones y adaptaciones.

Asimismo, las estrategias aplicadas permiten optimizar el rendimiento, reducir errores operativos y asegurar la calidad del servicio en un entorno multiusuario, garantizando la confiabilidad requerida en el ámbito universitario.  
En conjunto, estas acciones consolidan un sistema más estable, escalable y alineado con los principios de calidad, mantenibilidad y gestión del ciclo de vida del software establecidos por **Sommerville (2011)** y **Pressman (2010)**.  

De esta forma, el proyecto se configura como una solución tecnológica robusta y adaptable, capaz de sostener su funcionamiento en el tiempo y responder eficazmente a las necesidades institucionales y de los usuarios finales.
