# Casa de Cambio

## Autores
Lina Mariana Álvarez Góngora

Anderson Macias Gutiérrez

Nicole Dayan Polo Castro

## Fase 0:
Contextualización del enunciado del proyecto en donde se identifica:

**1. ¿Qué debemos hacer?**

Desarrollar un sistema de casa de cambio que permita gestionar clientes, operaciones financieras con tasas manuales y generar reportes para cumplimiento normativo.

**2. ¿Qué se necesita?**

•	Sistema de autenticación de usuarios

•	Sistema de registro y validación de clientes

•	Simulación y ejecución de operaciones de compra/venta con tasas manuales

•	Control de transacciones y reportes

**3. Elementos (objetos) que se identifican**

•	Bienvenida

•	Licencia

•	Cliente

•	Tasas manuales por operación 

•	Transaccion

•	Principal (Ventana principal con pestañas)

**4. ¿Qué objetos se incluye?**

• Bienvenida

• Licencia

• Principal

• Cliente

• Transaccion

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
| Nombre | R-03 Operaciones con Tasas Manuales |
|--------|-----------------------|
| Descripción | Permite ingresar tasa manual por operación para simulaciones de compra/venta |
| Entradas | Moneda Origen (selección: USD, EUR, COP), Moneda Destino (selección: USD, EUR, COP), Tasa manual (numérico), Monto (numérico) |
| Salidas | Cálculo de conversión, Detalle de simulación, Tasa aplicada en operación |


### R-04 Simulación de operaciones
| Nombre | R-04 Simulación de operaciones |
|--------|-----------------------|
| Descripción | Simular operaciones antes de confirmar, mostrando montos, tasas aplicadas y resultado |
| Entradas | Cliente (selección), Tipo de operación (Compra / Venta), Moneda de origen (Selección), Moneda de destino (Selección), Monto (númerico), Tasa manual (numérico) |
| Salidas | Detalle de simulación, Monto a recibir, Tasa aplicada |


### R-05 Ejecución de Transacciones 
| Nombre | R-05 Ejecución de transacciones |
|--------|-----------------------|
| Descripción | Regitrar transacciones confirmadas por clientes. |
| Entradas | Datos de simulacion confirmados|
| Salidas |Transaccion registrada, Comprobante de operación, Actualizacion de reportes |


### R-06 Generación de Reportes 
| Nombre | R-06 Generación de Reportes |
|--------|-----------------------|
| Descripción | Generar reportes de clientes, tasas y transacciones. |
| Entradas |Solicitud de reporte  |
| Salidas | Reporte completo del sistema, Listado de clientes, tasas y transacciones, Resumen financiero  |


### R-07 Gestión de Usuarios y Licencia 
| Nombre | R-07 Gestión de Usuarios y Licencia |
|--------|-----------------------|
| Descripción | Flujo de autenticación y aceptación de términos antes de acceder al sistema principal |
| Entradas | Nombre de usuario (texto),   |
| Salidas | Acceso al sistema principal, Personalización con nombre de usuario |


**Pseudocódigo Casa de Cambio**
```pseudocodigo

INICIO PROGRAMA
  // MÓDULO BIENVENIDA
  MOSTRAR ventana_bienvenida
  SOLICITAR nombre_usuario
  SI nombre_vacío ENTONCES mostrar_error
  nombre_capitalizado = CAPITALIZAR(nombre_usuario)
  GUARDAR nombre_global
  
  // MÓDULO LICENCIA
  MOSTRAR términos_condiciones
  SOLICITAR aceptación
  SI acepta ENTONCES ir_a_principal
  SINO volver_a_bienvenida

-------------------------------------------------------
// MÓDULO PRINCIPAL
CREAR pestañas: [Registro, Operaciones, Reportes]

// INICIALIZAR DATOS
clientes = []
transacciones = []

// PESTAÑA REGISTRO CLIENTE
AL REGISTRAR_CLIENTE:
  LEER nombre, documento, teléfono
  VALIDAR: campos_obligatorios, numérico(documento), numérico(teléfono), documento_único
  SI válido ENTONCES
    cliente_nuevo = Cliente(nombre, documento, teléfono)
    AGREGAR cliente_nuevo A clientes
    MOSTRAR confirmación
    ACTUALIZAR lista_clientes

-------------------------------------------------------
// PESTAÑA OPERACIONES
AL SIMULAR_OPERACIÓN:
  LEER cliente, tipo_operación, moneda_origen, moneda_destino, monto, tasa_manual
  VALIDAR: clientes_existen, tasa>0, monto>0, monedas_diferentes
  SI válido ENTONCES
    monto_destino = CALCULAR_CONVERSIÓN(moneda_origen, moneda_destino, monto, tasa)
    MOSTRAR simulación: cliente, tipo, monedas, montos, tasa

AL CONFIRMAR_OPERACIÓN:
  transacción = Transacción(cliente, tipo, monto, monto_destino, monedas, tasa)
  AGREGAR transacción A transacciones
  MOSTRAR comprobante
  LIMPIAR campos

FUNCIÓN CALCULAR_CONVERSIÓN(origen, destino, monto, tasa):
  SI (origen=EUR Y destino=USD) O (destino=COP) ENTONCES
    RETORNAR monto * tasa
  SINO SI (origen=USD Y destino=EUR) O (origen=COP) ENTONCES
    RETORNAR monto / tasa
  SINO
    RETORNAR monto * tasa
  FIN SI

-------------------------------------------------------
// PESTAÑA REPORTES
AL GENERAR_REPORTE:
  reporte = "REPORTE CASA DE CAMBIO\n"
  reporte += "Clientes: " + clientes.tamaño + "\n"
  PARA CADA cliente EN clientes:
    reporte += cliente.nombre + " - " + cliente.documento + "\n"
  
  reporte += "\nTransacciones: " + transacciones.tamaño + "\n"
  total = 0
  PARA CADA transacción EN transacciones:
    reporte += transacción.detalle + "\n"
    total += transacción.monto_origen
  
  reporte += "TOTAL: $" + total
  MOSTRAR reporte

-------------------------------------------------------
// FUNCIONES AUXILIARES
CAPITALIZAR(nombre): convertir primera letra de cada palabra a mayúscula
ES_NUMÉRICO(texto): verificar si es convertible a número

FIN PROGRAMA

```

**Diagarama de flujo**

![WhatsApp Image 2025-11-21 at 6 35 05 PM](https://github.com/user-attachments/assets/9561ea5f-83b7-4be0-92ff-db61d91d0058)

## Fase 2:
Etapa de diseño que permite determinar cuáles son las clases que conformaran el sistema

•	Elaborar lista de sustantivos del enunciado del proyecto para determinar cuáles son las clases del sistema.
 
  •	Bienvenida (autenticación)
 
  •	Principal (interfaz principal)
 
  •	Cliente (gestión de clientes)
 
  •	TasaCambio (tasas de divisas)
 
  •	Transaccion (operaciones)

•	Construir representación gráfica de las clases identificadas y asociar, las características a cada clase (atributos) y las operaciones que se van a realizar (métodos).

<table>
  <tr>
    <th colspan="2" style="text-align:center;">Bienvenida</th>
  </tr>
  <tr>
    <th>Atributos</th>
    <td>
      - texto: String (static)<br>
      - txtUsuario: JTextField<br>
      - btnIngresar: JButton
    </td>
  </tr>
  <tr>
    <th>Métodos</th>
    <td>
      + Bienvenida() (constructor)<br>
      + configurarEventos(): void<br>
      + main(String[] args): void
    </td>
  </tr>
</table>
---------------------------------------------------------------------------
<table>
  <tr>
    <th colspan="2" style="text-align:center;">Principal</th>
  </tr>

  <tr>
    <th>Atributos</th>
    <td>
      - clientes: ArrayList&lt;Cliente&gt;<br>
      - tasas: ArrayList&lt;TasaCambio&gt;<br>
      - transacciones: ArrayList&lt;Transaccion&gt;<br>
      - tabbedPane: JTabbedPane
    </td>
  </tr>

  <tr>
    <th>Métodos</th>
    <td>
      + Principal() (constructor)<br>
      + inicializarComponentes(): void<br>
      + configurarInterfaz(): void<br>
      + configurarEventos(): void<br>
      + registrarCliente(): void<br>
      + guardarTasas(): void<br>
      + simularOperacion(): void<br>
      + confirmarTransaccion(): void<br>
      + generarReporte(): void<br>
      + actualizarTipoOperacion(): void<br>
      + actualizarComboClientes(): void
    </td>
  </tr>
</table>
---------------------------------------------------------------------------
<table>
  <tr>
    <th colspan="2" style="text-align:center;">Cliente</th>
  </tr>

  <tr>
    <th>Atributos</th>
    <td>
      - nombre: String<br>
      - documento: String<br>
      - telefono: String
    </td>
  </tr>

  <tr>
    <th>Métodos</th>
    <td>
      + Cliente(String, String, String) (constructor)<br>
      + getNombre(): String<br>
      + getDocumento(): String<br>
      + getTelefono(): String<br>
      + toString(): String
    </td>
  </tr>
</table>
-----------------------------------------------------
<table>
  <tr>
    <th colspan="2" style="text-align:center;">TasaCambio</th>
  </tr>

  <tr>
    <th>Atributos</th>
    <td>
      - moneda: String<br>
      - tasaCompra: double<br>
      - tasaVenta: double<br>
      - fecha: String
    </td>
  </tr>

  <tr>
    <th>Métodos</th>
    <td>
      + TasaCambio(String, double, double, String) (constructor)<br>
      + getMoneda(): String<br>
      + getTasaCompra(): double<br>
      + getTasaVenta(): double<br>
      + getFecha(): String<br>
      + toString(): String
    </td>
  </tr>
</table>
---------------------------------------------
<table>
  <tr>
    <th colspan="2" style="text-align:center;">Transaccion</th>
  </tr>

  <tr>
    <th>Atributos</th>
    <td>
      - cliente: Cliente<br>
      - tipo: String<br>
      - montoOrigen: double<br>
      - montoDestino: double<br>
      - tasa: TasaCambio
    </td>
  </tr>

  <tr>
    <th>Métodos</th>
    <td>
      + Transaccion(Cliente, String, double, TasaCambio) (constructor)<br>
      + getCliente(): Cliente<br>
      + getTipo(): String<br>
      + getMontoOrigen(): double<br>
      + getMontoDestino(): double<br>
      + getTasa(): TasaCambio
    </td>
  </tr>
</table>

---------------------------------------------------

• Documentación atributos de la clase

<table>
  <tr>
    <th>Nombre de la clase</th>
    <th>Nombre del atributo</th>
    <th>Nombre Codificación</th>
    <th>Objetivo</th>
  </tr>

  <tr>
    <td rowspan="3">Bienvenida</td>
    <td>texto</td>
    <td>String (static)</td>
    <td>Almacena el nombre del usuario autenticado en el sistema</td>
  </tr>

  <tr>
    <td>txtUsuario</td>
    <td>JTextField</td>
    <td>Campo de entrada para que el usuario ingrese su nombre</td>
  </tr>

  <tr>
    <td>btnIngresar</td>
    <td>JButton</td>
    <td>Botón para validar y acceder al sistema principal</td>
  </tr>
</table>
-------------------------------------------------------------------------------------

<table>
  <tr>
    <th>Nombre de la clase</th>
    <th>Nombre del atributo</th>
    <th>Nombre Codificación</th>
    <th>Objetivo</th>
  </tr>

  <tr>
    <td rowspan="19">Principal</td>
    <td>clientes</td>
    <td>ArrayList&lt;Cliente&gt;</td>
    <td>Almacena la lista de todos los clientes registrados</td>
  </tr>

  <tr>
    <td>tasas</td>
    <td>ArrayList&lt;TasaCambio&gt;</td>
    <td>Contiene todas las tasas de cambio configuradas</td>
  </tr>

  <tr>
    <td>transacciones</td>
    <td>ArrayList&lt;Transaccion&gt;</td>
    <td>Registra el historial de todas las transacciones realizadas</td>
  </tr>

  <tr>
    <td>tabbedPane</td>
    <td>JTabbedPane</td>
    <td>Contenedor principal con las 4 pestañas de funcionalidad</td>
  </tr>

  <tr>
    <td>txtNombre</td>
    <td>JTextField</td>
    <td>Campo para ingresar el nombre del cliente</td>
  </tr>

  <tr>
    <td>txtDocumento</td>
    <td>JTextField</td>
    <td>Campo para ingresar el documento del cliente</td>
  </tr>

  <tr>
    <td>txtTelefono</td>
    <td>JTextField</td>
    <td>Campo para ingresar el teléfono del cliente</td>
  </tr>

  <tr>
    <td>comboMoneda</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de moneda para tasas (USD, EUR, COP)</td>
  </tr>

  <tr>
    <td>txtCompra</td>
    <td>JTextField</td>
    <td>Campo para ingresar tasa de compra</td>
  </tr>

  <tr>
    <td>txtVenta</td>
    <td>JTextField</td>
    <td>Campo para ingresar tasa de venta</td>
  </tr>

  <tr>
    <td>comboClientes</td>
    <td>JComboBox&lt;Cliente&gt;</td>
    <td>Lista desplegable de clientes para operaciones</td>
  </tr>

  <tr>
    <td>comboTipo</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de tipo de operación (COMPRA/VENTA)</td>
  </tr>

  <tr>
    <td>comboMonedaOrigen</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de moneda de origen para operaciones</td>
  </tr>

  <tr>
    <td>comboMonedaDestino</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de moneda de destino para operaciones</td>
  </tr>

  <tr>
    <td>txtMonto</td>
    <td>JTextField</td>
    <td>Campo para ingresar monto a cambiar</td>
  </tr>

  <tr>
    <td>textAreaResultado</td>
    <td>JTextArea</td>
    <td>Área para mostrar resultados de simulación</td>
  </tr>

  <tr>
    <td>textAreaTasas</td>
    <td>JTextArea</td>
    <td>Área para mostrar lista de tasas configuradas</td>
  </tr>

  <tr>
    <td>textAreaReportes</td>
    <td>JTextArea</td>
    <td>Área para mostrar reportes generados</td>
  </tr>

</table>
-----------------------------------------------------------------------------------------------------------------------------------------
<table>
  <tr>
    <th>Nombre de la clase</th>
    <th>Nombre del atributo</th>
    <th>Nombre Codificación</th>
    <th>Objetivo</th>
  </tr>

  <tr>
    <td rowspan="3">Cliente</td>
    <td>nombre</td>
    <td>String</td>
    <td>Almacena el nombre completo del cliente</td>
  </tr>

  <tr>
    <td>documento</td>
    <td>String</td>
    <td>Almacena el número de documento de identidad</td>
  </tr>

  <tr>
    <td>telefono</td>
    <td>String</td>
    <td>Almacena el número de teléfono de contacto</td>
  </tr>
</table>
------------------------------------------------------------------------------------------------------
<table>
  <tr>
    <th>Nombre de la clase</th>
    <th>Nombre del atributo</th>
    <th>Nombre Codificación</th>
    <th>Objetivo</th>
  </tr>

  <tr>
    <td rowspan="4">TasaCambio</td>
    <td>moneda</td>
    <td>String</td>
    <td>Tipo de moneda (USD, EUR, COP)</td>
  </tr>

  <tr>
    <td>tasaCompra</td>
    <td>double</td>
    <td>Valor de tasa para operaciones de COMPRA</td>
  </tr>

  <tr>
    <td>tasaVenta</td>
    <td>double</td>
    <td>Valor de tasa para operaciones de VENTA</td>
  </tr>

  <tr>
    <td>fecha</td>
    <td>String</td>
    <td>Fecha de vigencia de la tasa</td>
  </tr>
</table>
------------------------------------------------------------------------------------------------------
<table>
  <tr>
    <th>Nombre de la clase</th>
    <th>Nombre del atributo</th>
    <th>Nombre Codificación</th>
    <th>Objetivo</th>
  </tr>

  <tr>
    <td rowspan="5">Transaccion</td>
    <td>cliente</td>
    <td>Cliente</td>
    <td>Referencia al cliente que realiza la operación</td>
  </tr>

  <tr>
    <td>tipo</td>
    <td>String</td>
    <td>Tipo de operación (COMPRA o VENTA)</td>
  </tr>

  <tr>
    <td>montoOrigen</td>
    <td>double</td>
    <td>Monto original en la moneda de origen</td>
  </tr>

  <tr>
    <td>montoDestino</td>
    <td>double</td>
    <td>Monto resultante en la moneda de destino</td>
  </tr>

  <tr>
    <td>tasa</td>
    <td>TasaCambio</td>
    <td>Tasa de cambio utilizada en la operación</td>
  </tr>
</table>
------------------------------------------------------------------------------------------------------
