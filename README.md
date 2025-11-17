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

•	Sistema de autenticación de usuarios

•	Sistema de registro y validación de clientes

•	Gestión dinámica de tasas de cambio

•	Simulación y ejecución de operaciones de compra/venta

•	Control de transacciones y reportes

**3. Elementos (objetos) que se identifican**

•	Bienvenida

•	Cliente

•	TasaCambio

•	Transaccion

•	Principal (Ventana principal con pestañas)

**4. ¿Qué objetos se incluye?**

• Bienvenida - Maneja el login de usuarios

• Cliente - Gestiona información de clientes

• TasaCambio - Administra tasas de compra/venta

• Transaccion - Controla operaciones realizadas

• Principal - Interfaz principal con 4 pestañas

**5. ¿Cómo lo genera y que objetos se requiere?**

Se genera con un desarrollo orientado a objetos donde cada parte cumpla una tarea clara y se comuniquen entre sí. La ventana principal del programa es la que dirige todo pues pide los datos del cliente, consulta las tasas de cambio disponibles y con esa información realiza y registra la operación de compra o venta de moneda. Así, cada componente hace su parte de forma ordenada, lo que permite que el sistema sea fácil de entender, usar y mantener.

## Fase 1:
Elaborar listado de requerimientos del contexto planteado. Donde cada requerimiento se debe documentar haciendo uso de la siguiente tabla.

### R-01 Autenticación de Usuario
| Nombre | R-01 Autenticación de Usuario |
|--------|---------------------------|
| Descripción | Sistema debe permitir ingreso seguro con validación de identidad del operador |
| Entradas | Nombre de usuario (texto) |
| Salidas | Acceso al sistema principal, Mensaje de bienvenida personalizado, Interfaz con nombre de usuario |


### R-02 Registro de Clientes
| Nombre | R-02 Registro de Clientes |
|--------|---------------------------|
| Descripción | Sistema debe permitir registrar clientes con información básica |
| Entradas | Nombre completo (texto), Documento (numérico), Teléfono (numérico) |
| Salidas | Cliente registrado en el sistema, Mensaje de obligatoriedad |


### R-03 Gestión de tasa
| Nombre | R-03 Gestión de tasa |
|--------|-----------------------|
| Descripción | Configurar y actualizar tasas de compra/venta por moneda |
| Entradas | Moneda (selección: USD, EUR, COP), Tasa de compra (numérico), Tasa de venta (numérico), Fecha (texto) |
| Salidas | Tasas guardadas en sistema, Mensaje de confirmación, Lista actualizada de tasas |


### R-04 Simulación de operaciones
| Nombre | R-04 Simulación de operaciones |
|--------|-----------------------|
| Descripción | Simular operaciones antes de confirmar, mostrando montos y tasas aplicadas. |
| Entradas | Cliente (selección), Tipo de operación (Compra / Venta), Moneda de origen (Selección), Moneda de destino (Selección), Monto (númerico) |
| Salidas | Detalle de simulación, Monto a recibir, Tasa aplicada |


### R-05 Ejecución de Transacciones 
| Nombre | R-05 Ejecución de transacciones |
|--------|-----------------------|
| Descripción | Regitrar transacciones confirmadas por clientes. |
| Entradas | Datos de simulacion confirmados|
| Salidas |Transaccion registrada, Comprobante de operación, Actualizacion de historial |


### R-06 Generación de Reportes 
| Nombre | R-06 Generación de Reportes |
|--------|-----------------------|
| Descripción | Generar reportes de clientes, tasas y transacciones. |
| Entradas |Solicitud de reporte  |
| Salidas | Reporte completo del sistema, Listado de clientes, tasas y transacciones, Resumen financiero  |


## Fase 2:
