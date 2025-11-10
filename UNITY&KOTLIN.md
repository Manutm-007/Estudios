# Mega Chuleta para Examen de PMDM (Uds 1-5) - Ejercicios Resueltos

## Índice

1. [Ejercicios Unity - Fundamentos y Scripts](#ejercicios-unity---fundamentos-y-scripts)
2. [Ejercicios Unity - Movimiento y Colisiones](#ejercicios-unity---movimiento-y-colisiones)
3. [Ejercicios Unity - UI y Prefabs](#ejercicios-unity---ui-y-prefabs)
4. [Ejercicios Kotlin - Variables, Control de Flujo, Colecciones](#ejercicios-kotlin---variables-control-de-flujo-colecciones)
5. [Ejercicios Kotlin - Funciones y POO](#ejercicios-kotlin---funciones-y-poo)

---

## Ejercicios Unity - Fundamentos y Scripts

### Ejercicio 1: Crear un Script Básico

**Enunciado:** Crea un script en Unity que muestre un mensaje diferente en la consola cada vez que se inicie el juego (`Start`) y cada frame (`Update`). Adjúntalo a la `Main Camera`.

**Pasos:**
1.  **Abrir Unity Hub:** Ejecuta Unity Hub.
2.  **Abrir Proyecto:** Selecciona un proyecto existente o crea uno nuevo (p. ej., "TestTuNombre") y ábrelo.
3.  **Crear Carpeta:** En el Project Manager (ventana inferior izquierda), haz clic derecho en la carpeta `Assets`. Selecciona `Create → Folder`. Nómbrala `Scripts`.
4.  **Crear Script:** Haz clic derecho dentro de la carpeta `Scripts`. Selecciona `Create → MonoBehaviour Script`. Nómbralo `MensajeBasico`.
5.  **Editar Script:** Haz doble clic en `MensajeBasico.cs`. Se abrirá en tu editor de código (Visual Studio Community o Code).
6.  **Escribir Código:** Reemplaza el contenido por:
    ```csharp
    using UnityEngine;

    public class MensajeBasico : MonoBehaviour
    {
        // Start se llama antes del primer frame update
        void Start()
        {
            Debug.Log("¡Hola desde Start!");
        }

        // Update se llama una vez por frame
        void Update()
        {
            Debug.Log("Actualizando frame...");
        }
    }
    ```
7.  **Guardar Script:** Guarda los cambios en el editor de código (Ctrl+S).
8.  **Volver a Unity:** El editor de Unity debería haberse actualizado.
9.  **Adjuntar Script:** En la Hierarchy (ventana superior izquierda), selecciona `Main Camera`. En el Inspector (ventana derecha), arrastra el script `MensajeBasico` desde el Project Manager hasta el área vacía del Inspector de la `Main Camera`. El script ahora aparece como componente del GameObject.
10. **Ejecutar Juego:** Pulsa el botón ▶ (Play) en la barra superior del editor.
11. **Ver Resultado:** Observa la ventana `Console` (normalmente abajo). Deberías ver el mensaje de `Start` una vez y el mensaje de `Update` repetirse cada frame. Activa la opción `Collapse` en la Consola para agrupar mensajes repetidos.
12. **Detener Juego:** Pulsa el botón ▶ (Play) de nuevo para detener la ejecución.

### Ejercicio 2: Script con Variables Públicas

**Enunciado:** Crea un script con variables públicas de tipo `int`, `float`, y `string`. Muestra sus valores iniciales en `Start` y cámbialos en `Update` (incrementando números, concatenando cadenas). Adjúntalo a un GameObject vacío.

**Pasos:**
1.  **Crear Script:** En la carpeta `Scripts`, crea un nuevo script llamado `VariablesPublicas`.
2.  **Editar Script:**
    ```csharp
    using UnityEngine;

    public class VariablesPublicas : MonoBehaviour
    {
        // Variables públicas visibles en el Inspector
        public int numeroEntero = 10;
        public float numeroDecimal = 3.14f;
        public string texto = "Hola";

        private bool primeraVez = true; // Para mostrar solo una vez

        void Start()
        {
            Debug.Log($"Valores iniciales - Entero: {numeroEntero}, Decimal: {numeroDecimal}, Texto: {texto}");
        }

        void Update()
        {
            if (primeraVez)
            {
                primeraVez = false;
                Debug.Log("Variables cambiadas en Update:");
            }
            // Cambiar valores
            numeroEntero++;
            numeroDecimal += 0.1f;
            texto += "!";

            // Mostrar valores actuales (opcional, para ver el cambio constante)
            // Debug.Log($"Entero: {numeroEntero}, Decimal: {numeroDecimal}, Texto: {texto}");
        }
    }
    ```
3.  **Guardar y Volver a Unity.**
4.  **Crear GameObject Vacío:** En la Hierarchy, haz clic derecho. Selecciona `Create Empty`. Nómbralo `VariablesGO`.
5.  **Adjuntar Script:** Arrastra `VariablesPublicas.cs` al GameObject `VariablesGO`.
6.  **Ver Variables en Inspector:** Selecciona `VariablesGO`. En el Inspector, verás los campos `Numero Entero`, `Numero Decimal`, `Texto`. Puedes cambiar sus valores *antes* de ejecutar el juego.
7.  **Ejecutar Juego:** Pulsa Play. Mira la Consola. Debería mostrar los valores iniciales y luego un mensaje indicando que se han cambiado.
8.  **Detener Juego.**

### Ejercicio 3: Acceder a Otro GameObject y su Componente

**Enunciado:** Crea un script que acceda a otro GameObject específico (p. ej., `Main Camera`) y modifique su componente `Transform` (posición Y) cada frame.

**Pasos:**
1.  **Crear Script:** `Scripts → Create → MonoBehaviour Script → AccesoGameObject`
2.  **Editar Script:**
    ```csharp
    using UnityEngine;

    public class AccesoGameObject : MonoBehaviour
    {
        // Variable pública para asignar el GameObject objetivo en el Inspector
        public GameObject objetivoGO;

        // Variable para almacenar el componente Transform del objetivo
        private Transform objetivoTransform;

        void Start()
        {
            // Opción 1: Asignar manualmente en Inspector (más seguro)
            if (objetivoGO != null)
            {
                objetivoTransform = objetivoGO.GetComponent<Transform>();
            }

            // Opción 2: Buscar por nombre (menos eficiente)
            // objetivoGO = GameObject.Find("Main Camera");
            // if (objetivoGO != null) objetivoTransform = objetivoGO.transform;
        }

        void Update()
        {
            if (objetivoTransform != null)
            {
                // Modificar posición Y del objetivo (usando Time.time para movimiento suave)
                Vector3 nuevaPos = objetivoTransform.position;
                nuevaPos.y = Mathf.Sin(Time.time) * 2f; // Oscila entre -2 y 2
                objetivoTransform.position = nuevaPos;
            }
        }
    }
    ```
3.  **Guardar y Volver a Unity.**
4.  **Crear GameObject:** `Create Empty → Controlador`
5.  **Adjuntar Script:** `AccesoGameObject.cs` a `Controlador`.
6.  **Asignar Objetivo:** Selecciona `Controlador`. En el Inspector, verás el campo `Objetivo GO`. Arrastra `Main Camera` desde la Hierarchy hasta este campo.
7.  **Ejecutar Juego:** `Play`. La `Main Camera` debería moverse verticalmente de forma sinusoidal.
8.  **Detener Juego.**

---

## Ejercicios Unity - Movimiento y Colisiones

### Ejercicio 4: Movimiento con Input (Teclado)

**Enunciado:** Crea un script que permita mover un GameObject (p. ej., un `Cube`) en los ejes X y Z usando las teclas WASD o flechas. Usa `Time.deltaTime` para movimiento independiente del frame rate.

**Pasos:**
1.  **Crear Script:** `Scripts → Create → MonoBehaviour Script → MovimientoInput`
2.  **Editar Script:**
    ```csharp
    using UnityEngine;

    public class MovimientoInput : MonoBehaviour
    {
        public float velocidad = 5.0f; // Variable pública para ajustar velocidad en Inspector

        void Update()
        {
            // Capturar input de ejes
            float movimientoX = Input.GetAxis("Horizontal"); // A/D o <- ->
            float movimientoZ = Input.GetAxis("Vertical");   // W/S o Arriba/Abajo

            // Calcular desplazamiento
            Vector3 desplazamiento = new Vector3(movimientoX, 0, movimientoZ) * velocidad * Time.deltaTime;

            // Aplicar desplazamiento a la posición actual
            transform.Translate(desplazamiento);
        }
    }
    ```
3.  **Guardar y Volver a Unity.**
4.  **Crear GameObject:** `3D Object → Cube`
5.  **Adjuntar Script:** `MovimientoInput.cs` al `Cube`.
6.  **Ejecutar Juego:** `Play`. Usa WASD o flechas para mover el cubo.
7.  **Detener Juego.**

### Ejercicio 5: Movimiento Físico con Rigidbody

**Enunciado:** Crea un script que aplique fuerzas a un GameObject con `Rigidbody` para moverlo con Input. Asegúrate de usar `FixedUpdate`.

**Pasos:**
1.  **Crear Script:** `Scripts → Create → MonoBehaviour Script → MovimientoFisico`
2.  **Editar Script:**
    ```csharp
    using UnityEngine;

    public class MovimientoFisico : MonoBehaviour
    {
        public float fuerza = 10.0f;
        private Rigidbody rb;

        void Start()
        {
            // Obtener componente Rigidbody
            rb = GetComponent<Rigidbody>();
            if (rb == null)
            {
                Debug.LogError("Rigidbody no encontrado en " + gameObject.name);
            }
        }

        void FixedUpdate() // Importante usar FixedUpdate para física
        {
            float movimientoX = Input.GetAxis("Horizontal");
            float movimientoZ = Input.GetAxis("Vertical");

            Vector3 fuerzaAplicada = new Vector3(movimientoX, 0, movimientoZ) * fuerza;

            // Aplicar fuerza
            rb.AddForce(fuerzaAplicada);
        }
    }
    ```
3.  **Guardar y Volver a Unity.**
4.  **Crear GameObject:** `3D Object → Sphere`
5.  **Añadir Rigidbody:** Selecciona la `Sphere`. En el Inspector, `Add Component → Physics → Rigidbody`.
6.  **Adjuntar Script:** `MovimientoFisico.cs` a la `Sphere`.
7.  **Ejecutar Juego:** `Play`. Usa WASD o flechas para mover la esfera con física (más realista).
8.  **Detener Juego.**

### Ejercicio 6: Detectar Colisión (OnCollisionEnter)

**Enunciado:** Crea dos GameObjects (p. ej., `Cube` y `Sphere`). Asegúrate de que uno tenga `Rigidbody` y ambos tengan `Collider`. Crea un script para uno de ellos que detecte la colisión y muestre un mensaje.

**Pasos:**
1.  **Crear GameObjects:** `3D Object → Cube` y `3D Object → Sphere`. Colócalos cerca uno del otro, pero sin tocar.
2.  **Añadir Componentes:**
    *   Selecciona `Sphere`. Añade `Rigidbody`.
    *   Ambos (`Cube` y `Sphere`) ya tienen `Collider` por defecto (Box Collider y Sphere Collider respectivamente).
3.  **Crear Script:** `Scripts → Create → MonoBehaviour Script → DetectorColision`
4.  **Editar Script:**
    ```csharp
    using UnityEngine;

    public class DetectorColision : MonoBehaviour
    {
        void OnCollisionEnter(Collision other)
        {
            // other.gameObject es el otro objeto con el que colisionó
            Debug.Log("¡Colisión detectada con: " + other.gameObject.name + "!");
        }
    }
    ```
5.  **Guardar y Volver a Unity.**
6.  **Adjuntar Script:** Adjunta `DetectorColision.cs` a uno de los GameObjects, por ejemplo, al `Cube`.
7.  **Ejecutar Juego:** `Play`. La `Sphere` debería caer por gravedad y colisionar con el `Cube`. Mira la Consola.
8.  **Detener Juego.**

### Ejercicio 7: Detectar Trigger (OnTriggerEnter)

**Enunciado:** Crea un GameObject con `Collider` configurado como `Is Trigger`. Crea otro GameObject que lo atraviese. Usa un script para detectar cuando entra/sale del trigger.

**Pasos:**
1.  **Crear GameObjects:** `3D Object → Cube` (este será el trigger) y `3D Object → Sphere`.
2.  **Configurar Trigger:** Selecciona el `Cube`. En el Inspector, encuentra el componente `Box Collider`. Marca la casilla `Is Trigger`.
3.  **Crear Script:** `Scripts → Create → MonoBehaviour Script → DetectorTrigger`
4.  **Editar Script:**
    ```csharp
    using UnityEngine;

    public class DetectorTrigger : MonoBehaviour
    {
        void OnTriggerEnter(Collider other)
        {
            Debug.Log("¡Entró en el trigger: " + other.gameObject.name + "!");
        }

        void OnTriggerExit(Collider other)
        {
            Debug.Log("¡Salió del trigger: " + other.gameObject.name + "!");
        }
    }
    ```
5.  **Guardar y Volver a Unity.**
6.  **Adjuntar Script:** Adjunta `DetectorTrigger.cs` al `Cube` (el GameObject con el Collider como Trigger).
7.  **Posicionar:** Coloca la `Sphere` encima del `Cube` para que caiga a través de él.
8.  **Ejecutar Juego:** `Play`. La `Sphere` debería caer y atravesar el `Cube`, disparando los mensajes `OnTriggerEnter` y `OnTriggerExit`.
9.  **Detener Juego.**

---

## Ejercicios Unity - UI y Prefabs

### Ejercicio 8: Crear y Usar un Prefab

**Enunciado:** Crea un GameObject compuesto (p. ej., un `Cube` con un `Sphere` encima). Conviértelo en un Prefab. Luego, instancia varias copias del Prefab en la escena.

**Pasos:**
1.  **Crear GameObject Compuesto:**
    *   `3D Object → Cube`. Nómbralo `BloqueBase`.
    *   `3D Object → Sphere`. Nómbralo `TopSphere`.
    *   Arrastra `TopSphere` sobre `BloqueBase` en la Hierarchy para que sea hijo.
    *   Ajusta la posición de `TopSphere` (p. ej., `Y = 1`) para que esté encima de `BloqueBase`.
2.  **Crear Prefab:** Arrastra `BloqueBase` desde la Hierarchy hasta el Project Manager (dentro de `Assets` o una subcarpeta como `Prefabs`).
3.  **Usar Prefab:** En la Hierarchy, borra el `BloqueBase` original. Arrastra el nuevo asset `BloqueBase.prefab` desde el Project Manager a la Hierarchy o Scene View para crear una instancia.
4.  **Crear Más Instancias:** Arrastra el `BloqueBase.prefab` otras veces para crear más copias en la escena.
5.  **Modificar Prefab (Opcional):** Haz clic derecho en el asset `BloqueBase.prefab` en el Project Manager y selecciona `Open Prefab`. Cambia el color del `BloqueBase` en el Inspector (Material). Guarda (Ctrl+S). Vuelve a la escena principal. Verás que *todas* las instancias del prefab ahora tienen el nuevo color.

### Ejercicio 9: UI - Texto con Input

**Enunciado:** Crea un Canvas. Añade un TextMeshPro Text. Crea un script que cambie el texto del UI cada vez que se pulse la barra espaciadora.

**Pasos:**
1.  **Crear Canvas:** `UI → Canvas`.
2.  **Añadir TextMeshPro Text:** `UI → Text - TextMeshPro`. (Puede que necesites importar TMP Essentials si es la primera vez).
3.  **Crear Script:** `Scripts → Create → MonoBehaviour Script → TextoUIControl`
4.  **Editar Script:**
    ```csharp
    using UnityEngine;
    using TMPro; // Importar TextMeshPro

    public class TextoUIControl : MonoBehaviour
    {
        public TextMeshProUGUI textoUI; // Variable pública para el componente UI
        private int contador = 0;

        void Update()
        {
            if (Input.GetKeyDown(KeyCode.Space)) // Detectar pulsación de espacio
            {
                contador++;
                textoUI.text = "Veces pulsado: " + contador; // Cambiar texto
            }
        }
    }
    ```
5.  **Guardar y Volver a Unity.**
6.  **Adjuntar Script:** Adjunta `TextoUIControl.cs` a cualquier GameObject (p. ej., el `Canvas` o uno vacío).
7.  **Asignar Referencia UI:** Selecciona el GameObject con el script. En el Inspector, arrastra el GameObject `Text (TMP)` hasta el campo `Texto UI` del script.
8.  **Ejecutar Juego:** `Play`. Pulsa la barra espaciadora. El texto en pantalla debería aumentar.
9.  **Detener Juego.**

---

## Ejercicios Kotlin - Variables, Control de Flujo, Colecciones

### Ejercicio 10: Variables, Tipos, Conversión y Null Safety

**Enunciado:** Escribe un programa que:
1.  Declare una variable `var` de tipo `String` y asígnale un número como cadena (e.g., "123").
2.  Declare una variable `val` de tipo `Int` y asígnale el valor convertido de la cadena anterior.
3.  Declare una variable `var` de tipo `String?` (nullable) y asígnale `null`.
4.  Use el operador Elvis (`?:`) para asignar un valor por defecto si la variable nullable es `null`.
5.  Imprima los valores finales.

**Pasos:**
1.  **Abrir Android Studio.**
2.  **Crear Nuevo Proyecto o Abrir Uno Existente:** (p. ej., proyecto "Hola Mundo").
3.  **Crear Archivo Kotlin:** Haz clic derecho en el paquete (src/main/java/...). `New → Kotlin File/Class`. Nómbralo `EjercicioTipos`.
4.  **Escribir Código:**
    ```kotlin
    fun main() {
        // 1. Variable String con número
        var cadenaNumero: String = "123"

        // 2. Convertir a Int
        val numeroEntero: Int = cadenaNumero.toInt()

        // 3. Variable nullable
        var cadenaNula: String? = null

        // 4. Operador Elvis para valor por defecto
        val resultado = cadenaNula ?: "Valor por defecto"

        // 5. Imprimir
        println("Cadena original: $cadenaNumero")
        println("Número convertido: $numeroEntero")
        println("Variable nula: $cadenaNula")
        println("Resultado (con Elvis): $resultado")
    }
    ```
5.  **Ejecutar:** Haz clic derecho en el editor del archivo `EjercicioTipos.kt` y selecciona `Run 'EjercicioTiposKt'`.
6.  **Ver Salida:** Observa la consola de ejecución.

### Ejercicio 11: Control de Flujo (if, when, for, while)

**Enunciado:** Escribe un programa que:
1.  Use `if` como expresión para determinar si un número es positivo, negativo o cero.
2.  Use `when` para clasificar una calificación numérica (0-10) en una letra (A, B, C, D, F).
3.  Recorra una lista de números usando `for` y `forEach`.
4.  Use `while` para imprimir números del 10 al 1.

**Pasos:**
1.  **Crear Archivo:** `New → Kotlin File/Class → EjercicioControlFlujo`
2.  **Escribir Código:**
    ```kotlin
    fun main() {
        val numero = -5
        val calificacion = 8

        // 1. if como expresión
        val resultadoSigno = if (numero > 0) "positivo" else if (numero < 0) "negativo" else "cero"
        println("El número $numero es $resultadoSigno")

        // 2. when para calificación
        val letra = when (calificacion) {
            in 9..10 -> 'A'
            in 7..8 -> 'B'
            in 5..6 -> 'C'
            in 3..4 -> 'D'
            else -> 'F'
        }
        println("La calificación $calificacion es una $letra")

        // 3. Recorrer lista
        val numeros = listOf(1, 2, 3, 4, 5)
        println("Recorrido con for:")
        for (num in numeros) {
            print("$num ")
        }
        println() // Nueva línea

        println("Recorrido con forEach:")
        numeros.forEach { print("$it ") }
        println() // Nueva línea

        // 4. while descendente
        var contador = 10
        println("Conteo descendente con while:")
        while (contador > 0) {
            print("$contador ")
            contador--
        }
        println() // Nueva línea
    }
    ```
3.  **Ejecutar y Ver Salida.**

### Ejercicio 12: Colecciones (List, Map, filter, map)

**Enunciado:** Escribe un programa que:
1.  Cree una `List` de números enteros.
2.  Use `filter` para obtener solo los números pares.
3.  Use `map` para elevar al cuadrado los números filtrados.
4.  Cree un `Map` de personas (nombre -> edad).
5.  Imprima los resultados.

**Pasos:**
1.  **Crear Archivo:** `New → Kotlin File/Class → EjercicioColecciones`
2.  **Escribir Código:**
    ```kotlin
    fun main() {
        // 1. Crear lista
        val numeros = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

        // 2. Filtrar pares
        val pares = numeros.filter { it % 2 == 0 }

        // 3. Mapear al cuadrado
        val paresAlCuadrado = pares.map { it * it }

        println("Números originales: $numeros")
        println("Números pares: $pares")
        println("Pares al cuadrado: $paresAlCuadrado")

        // 4. Crear Map
        val personas = mapOf("Ana" to 25, "Luis" to 30, "Marta" to 22)

        // 5. Imprimir Map
        println("Personas:")
        for ((nombre, edad) in personas) {
            println("$nombre tiene $edad años")
        }
    }
    ```
3.  **Ejecutar y Ver Salida.**

---

## Ejercicios Kotlin - Funciones y POO

### Ejercicio 13: Funciones (Parámetros, Default, Lambda)

**Enunciado:** Escribe un programa que:
1.  Defina una función `saludar(nombre: String, idioma: String = "es")` que imprima un saludo en el idioma especificado (con valor por defecto).
2.  Defina una función `procesarLista(lista: List<Int>, operacion: (Int) -> Int)` que aplique una operación (lambda) a cada elemento.
3.  Llame a las funciones usando parámetros con nombre y pasando lambdas.

**Pasos:**
1.  **Crear Archivo:** `New → Kotlin File/Class → EjercicioFunciones`
2.  **Escribir Código:**
    ```kotlin
    fun saludar(nombre: String, idioma: String = "es") {
        when (idioma) {
            "es" -> println("Hola, $nombre")
            "en" -> println("Hello, $nombre")
            "fr" -> println("Bonjour, $nombre")
            else -> println("Saludo en idioma no soportado para $nombre")
        }
    }

    fun procesarLista(lista: List<Int>, operacion: (Int) -> Int): List<Int> {
        return lista.map(operacion)
    }

    fun main() {
        // 1. Llamar con valor por defecto
        saludar("Carlos")

        // 2. Llamar con parámetro con nombre
        saludar(nombre = "Marie", idioma = "fr")

        // 3. Lista y lambda
        val numeros = listOf(1, 2, 3, 4)
        val dobles = procesarLista(numeros) { it * 2 }
        val cuadrados = procesarLista(numeros, { num -> num * num }) // Sintaxis explícita

        println("Dobles: $dobles")
        println("Cuadrados: $cuadrados")
    }
    ```
3.  **Ejecutar y Ver Salida.**

### Ejercicio 14: POO Básica (Clase, Propiedades, Constructor, Métodos)

**Enunciado:** Define una clase `Libro` con propiedades `titulo` (String), `autor` (String), `anioPublicacion` (Int) y `disponible` (Boolean, por defecto `true`). Añade métodos `prestar()` y `devolver()`. Crea instancias y úsalas.

**Pasos:**
1.  **Crear Archivo:** `New → Kotlin File/Class → EjercicioPOO`
2.  **Escribir Código:**
    ```kotlin
    class Libro(val titulo: String, val autor: String, val anioPublicacion: Int, var disponible: Boolean = true) {

        fun prestar() {
            if (disponible) {
                disponible = false
                println("El libro '$titulo' ha sido prestado.")
            } else {
                println("El libro '$titulo' no está disponible.")
            }
        }

        fun devolver() {
            disponible = true
            println("El libro '$titulo' ha sido devuelto.")
        }

        override fun toString(): String {
            return "\"$titulo\" de $autor ($anioPublicacion) - Disponible: $disponible"
        }
    }

    fun main() {
        val libro1 = Libro("1984", "George Orwell", 1949)
        val libro2 = Libro("Cien años de soledad", "Gabriel García Márquez", 1967, disponible = false)

        println(libro1)
        println(libro2)

        libro1.prestar()
        println(libro1)

        libro2.prestar() // Intentar prestar uno no disponible

        libro1.devolver()
        println(libro1)
    }
    ```
3.  **Ejecutar y Ver Salida.**

### Ejercicio 15: Herencia y Clases Abstractas

**Enunciado:** Define una clase abstracta `Figura` con propiedades `color` (String) y un método abstracto `area(): Double`. Crea clases `Rectangulo` y `Circulo` que hereden de `Figura` y implementen `area`.

**Pasos:**
1.  **Crear Archivo:** `New → Kotlin File/Class → EjercicioHerencia`
2.  **Escribir Código:**
    ```kotlin
    abstract class Figura(val color: String) {
        abstract fun area(): Double
    }

    class Rectangulo(color: String, val base: Double, val altura: Double) : Figura(color) {
        override fun area(): Double {
            return base * altura
        }
    }

    class Circulo(color: String, val radio: Double) : Figura(color) {
        override fun area(): Double {
            return Math.PI * radio * radio
        }
    }

    fun main() {
        val rect = Rectangulo("Rojo", 5.0, 3.0)
        val circ = Circulo("Azul", 2.0)

        println("Área del rectángulo ${rect.color}: ${rect.area()}")
        println("Área del círculo ${circ.color}: ${circ.area()}")
    }
    ```
3.  **Ejecutar y Ver Salida.**

### Ejercicio 16: Data Class y Funciones de Alcance (`apply`, `let`)

**Enunciado:** Define una `data class` `Usuario` con `nombre`, `email`, y `edad`. Crea una instancia usando `apply` para configurarla. Usa `let` para imprimir un mensaje solo si `email` no es `null`.

**Pasos:**
1.  **Crear Archivo:** `New → Kotlin File/Class → EjercicioDataClass`
2.  **Escribir Código:**
    ```kotlin
    data class Usuario(val nombre: String, val email: String?, val edad: Int)

    fun main() {
        // Usar apply para configurar
        val usuario = Usuario(nombre = "Ana", email = "ana@example.com", edad = 28)

        // Usar let para operar si no es nulo
        usuario.email?.let { email ->
            println("Enviando correo a: $email")
        }

        // Imprimir objeto (gracias a data class)
        println(usuario)
    }
    ```
3.  **Ejecutar y Ver Salida.**
