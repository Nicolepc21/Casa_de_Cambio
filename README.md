# Casa de Cambio

## Autores
Lina Mariana Álvarez Góngora

Anderson Macias Gutiérrez

Nicole Dayan Polo Castro

## Fase 0:
Contextualización del enunciado del proyecto en donde se identifica:

**1. ¿Qué debemos hacer?**

Desarrollar un sistema de casa de cambio que permita gestionar clientes, tasas de cambio, operaciones financieras y generar reportes para cumplimiento normativo.

**2. ¿Qué se necesita?**

•	Sistema de registro de clientes

•	Gestión dinámica de tasas de cambio

•	Simulación y ejecución de operaciones de compra/venta

•	Control de transacciones y reportes

**3. Elementos (objetos) que se identifican**

•	Cliente

•	TasaCambio

•	Transaccion

•	CasaCambioGUI

**4. ¿Qué objetos se incluye?**

Cliente

TasaCambio

Transaccion

CasaCambioGUI

**5. ¿Cómo lo genera y que objetos se requiere?**

Se genera con un desarrollo orientado a objetos donde cada parte cumpla una tarea clara y se comuniquen entre sí. La ventana principal del programa (CasaCambioGUI) es la que dirige todo pues pide los datos del cliente, consulta las tasas de cambio disponibles y con esa información realiza y registra la operación de compra o venta de moneda. Así, cada componente hace su parte de forma ordenada, lo que permite que el sistema sea fácil de entender, usar y mantener.

## Fase 1:
Elaborar listado de requerimientos del contexto planteado. Donde cada requerimiento se debe documentar haciendo uso de la siguiente tabla.

### R-01 Registro de Clientes
| Nombre | R-01 Registro de Clientes |
|--------|---------------------------|
| Descripción | Sistema debe permitir registrar clientes con información básica |
| Entradas | Nombre completo (texto), Documento (numérico), Teléfono (numérico) |
| Salidas | Cliente registrado en el sistema, Mensaje de obligatoriedad |


### R-02 Gestión de tasa
| Nombre | R-02 Gestión de tasa |
|--------|-----------------------|
| Descripción | Configurar y actualizar tasas de compra/venta por moneda |
| Entradas | Moneda (selección: USD, EUR, COP), Tasa de compra (numérico), Tasa de venta (numérico), Fecha (texto) |
| Salidas | Tasas guardadas en sistema, Mensaje de confirmación, Lista actualizada de tasas |


### R-03 Simulación de operaciones
| Nombre | R-03 Simulación de operaciones |
|--------|-----------------------|
| Descripción | Simular operaciones antes de confirmar, mostrando montos y tasas aplicadas. |
| Entradas | Cliente (selección), Tipo de operación (Compra / Venta), Moneda de origen (Selección), Moneda de destino (Selección), Monto (númerico) |
| Salidas | Detalle de simulación, Monto a recibir, Tasa aplicada |


### R-04 Ejecución de Transacciones 
| Nombre | R-04 Ejecución de transacciones |
|--------|-----------------------|
| Descripción | Regitrar transacciones confirmadas por clientes. |
| Entradas | Datos de simulacion confirmados|
| Salidas |Transaccion registrada, Comprobante de operación, Actualizacion de historial |


### R-05 Generación de Reportes 
| Nombre | R-05 Generación de Reportes |
|--------|-----------------------|
| Descripción | Generar reportes de clientes, tasas y transacciones. |
| Entradas |Solicitud de reporte  |
| Salidas | Reporte completo del sistema, Listado de clientes, tasas y transacciones, Resumen financiero  |
