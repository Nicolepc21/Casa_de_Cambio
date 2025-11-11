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


**5. ¿Cómo lo genera y que objetos se requiere?**


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
