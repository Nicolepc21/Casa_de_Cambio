# Casa de cambio

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
 
  •	Bienvenida - Autenticación inicial

  •	Licencia - Aceptación de términos

  •	Principal - Interfaz principal del sistema

  •	Cliente - Gestión de datos de clientes

  •	Transaccion - Registro de operaciones

•	Construir representación gráfica de las clases identificadas y asociar, las características a cada clase (atributos) y las operaciones que se van a realizar (métodos).

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th colspan="1">Bienvenida</th>
  </tr>
  <tr>
    <td>
      <strong>Atributos</strong><br>
      - texto: <em>String</em> (static)<br>
      - txtUsuario: <em>JTextField</em><br>
      - btnIngresar: <em>JButton</em>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Métodos</strong><br>
      + Bienvenida() <em>(constructor)</em><br>
      + configurarInterface(): <em>void</em><br>
      + configurarEventos(): <em>void</em><br>
      + capitalizarNombreCompleto(String): <em>String</em><br>
      + main(String[]): <em>void</em>
    </td>
  </tr>
</table>

---------------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th colspan="1">Licencia</th>
  </tr>

  <tr>
    <td>
      <strong>Atributos</strong><br>
      - checkAceptar: <em>JCheckBox</em><br>
      - btnContinuar: <em>JButton</em><br>
      - btnNoAcepto: <em>JButton</em>
    </td>
  </tr>

  <tr>
    <td>
      <strong>Métodos</strong><br>
      + Licencia()<br>
      + configurarInterfaz(): <em>void</em><br>
      + configurarEventos(): <em>void</em>
    </td>
  </tr>
</table>

---------------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th colspan="1">Principal</th>
  </tr>

  <tr>
    <td>
      <strong>Atributos</strong><br>
      - clientes: <em>ArrayList&lt;Cliente&gt;</em><br>
      - transacciones: <em>ArrayList&lt;Transaccion&gt;</em><br>
      - txtNombre, txtDocumento, txtTelefono: <em>JTextField</em><br>
      - btnRegistrarCliente: <em>JButton</em><br>
      - comboClientes: <em>JComboBox&lt;Cliente&gt;</em><br>
      - comboTipo: <em>JComboBox&lt;String&gt;</em><br>
      - comboMonedaOrigen, comboMonedaDestino: <em>JComboBox&lt;String&gt;</em><br>
      - txtMonto, txtTasa: <em>JTextField</em><br>
      - textAreaResultado, textAreaReportes: <em>JTextArea</em><br>
      - btnSimular, btnConfirmar, btnGenerarReporte: <em>JButton</em><br>
      - tabbedPane: <em>JTabbedPane</em>
    </td>
  </tr>

  <tr>
    <td>
      <strong>Métodos</strong><br>
      + Principal()<br>
      + inicializarComponentes(): <em>void</em><br>
      + configurarInterface(): <em>void</em><br>
      + configurarEventos(): <em>void</em><br>
      + crearPanelRegistroCliente(): <em>JPanel</em><br>
      + crearPanelOperaciones(): <em>JPanel</em><br>
      + crearPanelReportes(): <em>JPanel</em><br>
      + actualizarTipoOperacion(): <em>void</em><br>
      + esNumerico(String): <em>boolean</em><br>
      + actualizarComboClientes(): <em>void</em><br>
      + capitalizarNombreCompleto(String): <em>String</em><br>
      + registrarCliente(): <em>void</em><br>
      + simularOperacion(): <em>void</em><br>
      + confirmarTransaccion(): <em>void</em><br>
      + generarReporte(): <em>void</em><br>
      + main(String[]): <em>void</em>
    </td>
  </tr>
</table>

---------------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th colspan="1">Cliente</th>
  </tr>

  <tr>
    <td>
      <strong>Atributos</strong><br>
      - nombre: <em>String</em><br>
      - documento: <em>String</em><br>
      - telefono: <em>String</em>
    </td>
  </tr>

  <tr>
    <td>
      <strong>Métodos</strong><br>
      + Cliente(String, String, String)<br>
      + getNombre(): <em>String</em><br>
      + getDocumento(): <em>String</em><br>
      + getTelefono(): <em>String</em><br>
      + setNombre(String): <em>void</em><br>
      + setDocumento(String): <em>void</em><br>
      + setTelefono(String): <em>void</em><br>
      + toString(): <em>String</em>
    </td>
  </tr>
</table>

---------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th colspan="1">Transaccion</th>
  </tr>

  <tr>
    <td>
      <strong>Atributos</strong><br>
      - cliente: <em>Cliente</em><br>
      - tipo: <em>String</em><br>
      - montoOrigen: <em>double</em><br>
      - montoDestino: <em>double</em><br>
      - tasaAplicada: <em>double</em><br>
      - monedaOrigen: <em>String</em><br>
      - monedaDestino: <em>String</em><br>
      - fecha: <em>String</em>
    </td>
  </tr>

  <tr>
    <td>
      <strong>Métodos</strong><br>
      + Transaccion(Cliente, String, double, double, String, String, double)<br>
      + getCliente(): <em>Cliente</em><br>
      + getTipo(): <em>String</em><br>
      + getMontoOrigen(): <em>double</em><br>
      + getMontoDestino(): <em>double</em><br>
      + getTasaAplicada(): <em>double</em><br>
      + getMonedaOrigen(): <em>String</em><br>
      + getMonedaDestino(): <em>String</em><br>
      + getFecha(): <em>String</em><br>
      + toString(): <em>String</em>
    </td>
  </tr>
</table>

---------------------------------------------------

• Documentación atributos de la clase

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Clase</th>
    <th>Atributo</th>
    <th>Tipo</th>
    <th>Objetivo</th>
  </tr>

  <tr>
    <td rowspan="3">Bienvenida</td>
    <td>texto</td>
    <td>String (static)</td>
    <td>Almacena nombre del usuario</td>
  </tr>

  <tr>
    <td>txtNombre</td>
    <td>JTextField</td>
    <td>Campo para ingresar nombre</td>
  </tr>

  <tr>
    <td>btnIngresar</td>
    <td>JButton</td>
    <td>Botón para acceder</td>
  </tr>
</table>

-------------------------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Clase</th>
    <th>Atributo</th>
    <th>Tipo</th>
    <th>Descripción</th>
  </tr>

  <tr>
    <td rowspan="20">Principal</td>
    <td>clientes</td>
    <td>ArrayList&lt;Cliente&gt;</td>
    <td>Lista dinámica de clientes registrados</td>
  </tr>

  <tr>
    <td>transacciones</td>
    <td>ArrayList&lt;Transaccion&gt;</td>
    <td>Historial de transacciones realizadas</td>
  </tr>

  <tr>
    <td>tabbedPane</td>
    <td>JTabbedPane</td>
    <td>Contenedor principal con pestañas</td>
  </tr>

  <tr>
    <td>txtNombre</td>
    <td>JTextField</td>
    <td>Campo para nombre del cliente</td>
  </tr>

  <tr>
    <td>txtDocumento</td>
    <td>JTextField</td>
    <td>Campo para documento del cliente</td>
  </tr>

  <tr>
    <td>txtTelefono</td>
    <td>JTextField</td>
    <td>Campo para teléfono del cliente</td>
  </tr>

  <tr>
    <td>btnRegistrarCliente</td>
    <td>JButton</td>
    <td>Botón para registrar nuevo cliente</td>
  </tr>

  <tr>
    <td>comboClientes</td>
    <td>JComboBox&lt;Cliente&gt;</td>
    <td>Lista desplegable de clientes</td>
  </tr>

  <tr>
    <td>comboTipo</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de tipo (COMPRA/VENTA)</td>
  </tr>

  <tr>
    <td>comboMonedaOrigen</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de moneda origen (USD, EUR, COP)</td>
  </tr>

  <tr>
    <td>comboMonedaDestino</td>
    <td>JComboBox&lt;String&gt;</td>
    <td>Selector de moneda destino (USD, EUR, COP)</td>
  </tr>

  <tr>
    <td>txtMonto</td>
    <td>JTextField</td>
    <td>Campo para monto a convertir</td>
  </tr>

  <tr>
    <td>txtTasa</td>
    <td>JTextField</td>
    <td>Campo para tasa manual de operación</td>
  </tr>

  <tr>
    <td>textAreaResultado</td>
    <td>JTextArea</td>
    <td>Área para mostrar resultados simulación</td>
  </tr>

  <tr>
    <td>btnSimular</td>
    <td>JButton</td>
    <td>Botón para simular operación</td>
  </tr>

  <tr>
    <td>btnConfirmar</td>
    <td>JButton</td>
    <td>Botón para confirmar transacción</td>
  </tr>

  <tr>
    <td>textAreaReportes</td>
    <td>JTextArea</td>
    <td>Área para mostrar reportes generados</td>
  </tr>

  <tr>
    <td>btnGenerarReporte</td>
    <td>JButton</td>
    <td>Botón para generar reporte del sistema</td>
  </tr>

  <tr>
    <td>lblUsuario</td>
    <td>JLabel</td>
    <td>Etiqueta con nombre usuario activo</td>
  </tr>

  <tr>
    <td>btnSalir</td>
    <td>JButton</td>
    <td>Botón para cerrar sesión</td>
  </tr>

</table>

-----------------------------------------------------------------------------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Clase</th>
    <th>Atributo</th>
    <th>Tipo</th>
    <th>Descripción</th>
  </tr>

  <tr>
    <td rowspan="3">Cliente</td>
    <td>nombre</td>
    <td>String</td>
    <td>Nombre completo del cliente</td>
  </tr>

  <tr>
    <td>documento</td>
    <td>String</td>
    <td>Número de documento de identidad</td>
  </tr>

  <tr>
    <td>telefono</td>
    <td>String</td>
    <td>Número de teléfono de contacto</td>
  </tr>
</table>

------------------------------------------------------------------------------------------------------
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Clase</th>
    <th>Atributo</th>
    <th>Tipo</th>
    <th>Descripción</th>
  </tr>

  <tr>
    <td rowspan="8">Transaccion</td>
    <td>cliente</td>
    <td>Cliente</td>
    <td>Referencia al cliente de la operación</td>
  </tr>

  <tr>
    <td>tipo</td>
    <td>String</td>
    <td>Tipo de operación (COMPRA o VENTA)</td>
  </tr>

  <tr>
    <td>montoOrigen</td>
    <td>double</td>
    <td>Monto original en moneda de origen</td>
  </tr>

  <tr>
    <td>montoDestino</td>
    <td>double</td>
    <td>Monto resultante en moneda destino</td>
  </tr>

  <tr>
    <td>tasaAplicada</td>
    <td>double</td>
    <td>Tasa manual aplicada en la operación</td>
  </tr>

  <tr>
    <td>monedaOrigen</td>
    <td>String</td>
    <td>Código moneda origen (USD, EUR, COP)</td>
  </tr>

  <tr>
    <td>monedaDestino</td>
    <td>String</td>
    <td>Código moneda destino (USD, EUR, COP)</td>
  </tr>

  <tr>
    <td>fecha</td>
    <td>String</td>
    <td>Fecha de realización de la transacción</td>
  </tr>

</table>

## Fase 3:
En esta fase se da inicio a la codificación de las clases diseñadas en la fase II

•	Codificación de los atributos teniendo en cuenta el tipo y la visibilidad
### Clase Bienvenida
```Bienvenida
public class Bienvenida extends JFrame {
    // ATRIBUTOS CON VISIBILIDAD
    public static String texto = "";                    // public static - compartido entre ventanas
    private JTextField txtNombre;                       // private - campo entrada nombre
    private JButton btnIngresar;                        // private - botón acceso sistema
    private JLabel lblTitulo;                           // private - título ventana
    private JLabel lblInstruccion;                      // private - instrucciones usuario
    
    // MÉTODOS PRINCIPALES
    public Bienvenida() {                               // public - constructor
        configurarInterfaz();
        configurarEventos();
    }
    
    private void configurarInterfaz() { ... }           // private - diseño UI
    private void configurarEventos() { ... }            // private - manejo eventos
    private String capitalizarNombreCompleto(String nombre) { ... } // private - formato nombre
    public static void main(String[] args) { ... }      // public static - punto entrada
}
```
### Clase Licencia
```Licencia
public class Licencia extends JFrame {
    // ATRIBUTOS CON VISIBILIDAD
    private JCheckBox checkAceptar;                     // private - aceptación términos
    private JButton btnContinuar;                       // private - botón continuar
    private JButton btnNoAcepto;                        // private - botón rechazar
    private JTextArea textoLicencia;                    // private - texto términos
    private JLabel lblTitulo;                           // private - título ventana
    private JScrollPane scrollLicencia;                 // private - scroll área texto
    
    // MÉTODOS PRINCIPALES
    public Licencia() {                                 // public - constructor
        configurarInterfaz();
        configurarEventos();
    }
    
    private void configurarInterfaz() { ... }           // private - diseño UI
    private void configurarEventos() { ... }            // private - manejo eventos
}
```

•	Codificación de los atributos teniendo en cuenta el tipo y la visibilidad

### Clase Bienvenida
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del método</th>
    <th>Bienvenida</th>
  </tr>

  <tr>
    <td>Entrada (lista de Parámetros)</td>
    <td>Ninguno</td>
  </tr>

  <tr>
    <td>Resultado (tipo de dato de retorno)</td>
    <td>void (constructor)</td>
  </tr>

  <tr>
    <td>Solución planteada</td>
    <td>Inicializa la ventana de bienvenida y configura interfaz y eventos</td>
  </tr>

  <tr>
    <td>Firma del Método</td>
    <td>public Bienvenida()</td>
  </tr>
</table>
--------------------------------------------------------------------------------------------------------------------------

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del método</th>
    <th>configurarInterfaz</th>
  </tr>

  <tr>
    <td>Entrada (lista de Parámetros)</td>
    <td>Ninguno</td>
  </tr>

  <tr>
    <td>Resultado (tipo de dato de retorno)</td>
    <td>void</td>
  </tr>

  <tr>
    <td>Solución planteada</td>
    <td>Configura todos los componentes visuales de la ventana</td>
  </tr>

  <tr>
    <td>Firma del Método</td>
    <td>private void configurarInterfaz()</td>
  </tr>
</table>
-------------------------------------------------------------------------------------------------------

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del Método</th>
    <td>configurarEventos</td>
  </tr>

  <tr>
    <th>Entrada (lista de Parámetros)</th>
    <td>Ninguno</td>
  </tr>

  <tr>
    <th>Resultado (tipo de dato de retorno)</th>
    <td>Void</td>
  </tr>

  <tr>
    <th>Solución planteada</th>
    <td>Define el comportamiento de botones y campos de texto</td>
  </tr>

  <tr>
    <th>Firma del Método</th>
    <td>private void configurarEventos()</td>
  </tr>
</table>
--------------------------------------------------------------------------------------------------------

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del Método</th>
    <th>capitalizarNombreCompleto</th>
  </tr>

  <tr>
    <td>Entrada (lista de Parámetros)</td>
    <td>nombre: String</td>
  </tr>

  <tr>
    <td>Resultado (tipo de dato de retorno)</td>
    <td>String</td>
  </tr>

  <tr>
    <td>Solución planteada</td>
    <td>Convierte un nombre a formato con primera letra mayúscula</td>
  </tr>

  <tr>
    <td>Firma del Método</td>
    <td>private String capitalizarNombreCompleto(String nombre)</td>
  </tr>
</table>
---------------------------------------------------------------------------------------------------------

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del Método</th>
    <td>main</td>
  </tr>

  <tr>
    <th>Entrada (lista de Parámetros)</th>
    <td>args: String[]</td>
  </tr>

  <tr>
    <th>Resultado (tipo de dato de retorno)</th>
    <td>Void</td>
  </tr>

  <tr>
    <th>Solución planteada</th>
    <td>Punto de entrada principal de la aplicación</td>
  </tr>

  <tr>
    <th>Firma del Método</th>
    <td>public static void main(String[] args)</td>
  </tr>
</table>
----------------------------------------------------------------------------------------------------------

### Clase Licencia
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del Método</th>
    <th>Licencia</th>
  </tr>

  <tr>
    <td>Entrada (lista de Parámetros)</td>
    <td>Ninguno</td>
  </tr>

  <tr>
    <td>Resultado (tipo de dato de retorno)</td>
    <td>Void (constructor)</td>
  </tr>

  <tr>
    <td>Solución planteada</td>
    <td>Inicializa ventana de licencia y configura componentes</td>
  </tr>

  <tr>
    <td>Firma del Método</td>
    <td>public Licencia()</td>
  </tr>
</table>
-------------------------------------------------------------------------------------------------------------------------

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del Método</th>
    <td>configurarInterfaz</td>
  </tr>

  <tr>
    <th>Entrada (lista de Parámetros)</th>
    <td>Ninguno</td>
  </tr>

  <tr>
    <th>Resultado (tipo de dato de retorno)</th>
    <td>void</td>
  </tr>

  <tr>
    <th>Solución planteada</th>
    <td>Diseña la interfaz de la ventana de términos y condiciones</td>
  </tr>

  <tr>
    <th>Firma del Método</th>
    <td>private void configurarInterfaz()</td>
  </tr>
</table>
---------------------------------------------------------------------------------------------------------------------------

<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Nombre del Método</th>
    <td>configurarEventos</td>
  </tr>

  <tr>
    <th>Entrada (lista de Parámetros)</th>
    <td>Ninguno</td>
  </tr>

  <tr>
    <th>Resultado (tipo de dato de retorno)</th>
    <td>void</td>
  </tr>

  <tr>
    <th>Solución planteada</th>
    <td>Configura eventos de checkboxes y botones de la licencia</td>
  </tr>

  <tr>
    <th>Firma del Método</th>
    <td>private void configurarEventos()</td>
  </tr>
</table>
-----------------------------------------------------------------------------------------------------------------------------

•	Diseño de prototipos de entrada y la salida de datos correspondiente a la interfaz del usuario.
<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/5b2ec7aa-8147-433c-bd53-2a0b4b256b6f" />
<img width="700" height="900" alt="image" src="https://github.com/user-attachments/assets/f81ada5a-6cf7-4bc7-bfa9-39436846b7cc" />
<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/5f11f6a4-91c5-448f-9795-5ba054ecb77d" />
<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/fdb51834-09fc-4b98-80d8-07caae57c2ba" />

## Fase 4:
• Implementación de los métodos ( construcción de la parte lógica )

  • Codificación de formulas

  •	Asignaciones

  •	Condicionales


### Cálculo de Conversión de Divisas
```calculo
public double calcularConversion(String monedaOrigen, String monedaDestino, 
                                double monto, double tasaManual) {
    double resultado = 0.0;
    
    if ("EUR".equals(monedaOrigen) && "USD".equals(monedaDestino)) {
        resultado = monto * tasaManual;                    // EUR → USD
    } else if ("USD".equals(monedaOrigen) && "EUR".equals(monedaDestino)) {
        resultado = monto / tasaManual;                    // USD → EUR
    } else if ("COP".equals(monedaOrigen)) {
        resultado = monto / tasaManual;                    // COMPRA divisas
    } else if ("COP".equals(monedaDestino)) {
        resultado = monto * tasaManual;                    // VENTA divisas
    } else {
        resultado = monto * tasaManual;                    // Default
    }
    
    return resultado;
}
```
### Validación campos numéricos
```validacion
public boolean esNumerico(String texto) {
    if (texto == null || texto.trim().isEmpty()) {
        return false;
    }
    try {
        Double.parseDouble(texto.trim());
        return true;
    } catch (NumberFormatException e) {
        return false;
    }
}
```
### Generación de reportes
```reportes
public String generarReporteConsolidado() {
    StringBuilder reporte = new StringBuilder();
    
    // Encabezado
    reporte.append("REPORTE CASA DE CAMBIO\n");
    reporte.append("═══════════════════════════════\n\n");
    
    // Sección clientes
    reporte.append("CLIENTES REGISTRADOS: ").append(clientes.size()).append("\n");
    
    // Sección transacciones con totales
    double totalTransacciones = transacciones.stream()
        .mapToDouble(Transaccion::getMontoOrigen)
        .sum();
    
    reporte.append("TOTAL MOVILIZADO: $")
          .append(String.format("%,.2f", totalTransacciones))
          .append("\n");
    
    return reporte.toString();
}
```
• Documentación aplicación utilizando javadoc

Se encuentra desarrollado durante todo el código

## Fase 5:
•	Adjuntar evidencias de resultados de la ejecución (pantallazos).

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/098002e6-3c0b-40db-b501-87d80d120276" />
<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/bdbb0282-491f-45ac-aea9-f8c6c70e19b5" />
<img width="400" height="350" alt="image" src="https://github.com/user-attachments/assets/d18d42ec-4f42-4d1a-94cf-d6efc9b5b9c1" />
<img width="400" height="350" alt="image" src="https://github.com/user-attachments/assets/c7869196-1fd5-4a51-b960-e2d12310e74b" />
<img width="400" height="350" alt="image" src="https://github.com/user-attachments/assets/796971d1-a00c-4938-bc96-090a5004d438" />
<img width="400" height="350" alt="image" src="https://github.com/user-attachments/assets/971f6b2c-9941-4552-802e-c7ea1b3984c3" />
<img width="400" height="350" alt="image" src="https://github.com/user-attachments/assets/0e8fcae1-4910-4caa-a634-11598ad21c32" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/f9221483-00e6-4cfa-8ed8-054c5b6b57ec" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/a0a3b1d8-8ff6-4f41-9cf3-812d27ae298f" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/f5777dd4-97ba-4d75-9c53-9d14e628373c" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/fdb9ac67-aed6-457c-97a1-b6edfd2669db" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/f7aa0240-0f05-4ad3-b09a-1bb4ea292471" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/98ffffa3-3f5d-4f7c-888d-2b5f8faf2a3f" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/52587e66-f746-4972-939c-e1a1784142bc" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/b994a9ff-6c12-405b-8000-9de0f1052e00" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/8cf75073-88a3-44ed-b05e-b1dd6aca3d76" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/5470e2b1-2670-4566-8f4d-8b31d0898171" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ac5cdf56-3961-4a43-be99-194b295b5e9e" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/8df7ef8e-fd89-4af3-ac97-cff01b36c211" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/304b920c-4c84-4c19-8519-3ec4abf8f8e8" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/30714ce8-d628-409e-89be-f3cf602cdbcc" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/a102e43f-47a8-4d47-bd36-25a52b28aa52" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/2d02f5b2-fb14-42aa-ace0-6117f19c5505" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/f07f1945-c280-4976-93d6-90a9ab3eac31" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/32765dd0-55fa-4072-a508-eccfcc42686a" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/534fef03-35a2-4d25-a430-bb9d220faec1" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/5aefa97e-8962-4d20-9757-1c45999bc405" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/9b5d7974-f65d-4f63-87d3-f9d929e59af7" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/3d0249db-1100-49d9-8a32-6faaba3fb827" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/a110e2c3-9c3f-4ff3-8dc9-60645a6d1928" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/af47d219-7f1e-4b57-96bc-27a1c02b9a49" />
<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/26f47e83-ff08-41f0-aa22-d4b64bc8d2f5" />


























