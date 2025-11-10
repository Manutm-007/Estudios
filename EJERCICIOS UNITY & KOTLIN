Ejercicio 17: UI - Puntuación con Botón

Enunciado: Crea una UI con un TextMeshPro Text que muestre una puntuación. Añade un botón. Cada vez que se pulse el botón, la puntuación debe aumentar en 10 puntos.

Pasos:

Crear Canvas: UI → Canvas.
Añadir TextMeshPro Text: UI → Text - TextMeshPro. Cámbiale el nombre a PuntuacionText en la Hierarchy. Cámbiale el texto en el Inspector a "Puntuación: 0".
Añadir Botón: UI → Button. Cámbiale el nombre a BotonSumar en la Hierarchy.
Crear Script: Scripts → Create → MonoBehaviour Script → ControladorPuntuacion
Editar Script:
using UnityEngine;
using TMPro; // Importar TextMeshPro
using UnityEngine.UI; // Importar UI

public class ControladorPuntuacion : MonoBehaviour
{
    public TextMeshProUGUI puntuacionText; // Referencia al texto UI
    public Button botonSumar; // Referencia al botón UI

    private int puntuacion = 0; // Variable interna para la puntuación

    void Start()
    {
        // Asignar la función al evento de click del botón
        botonSumar.onClick.AddListener(SumarPuntos);
    }

    // Función que se llama al pulsar el botón
    public void SumarPuntos()
    {
        puntuacion += 10;
        puntuacionText.text = "Puntuación: " + puntuacion;
    }
}
Guardar y Volver a Unity.
Adjuntar Script: Adjunta ControladorPuntuacion.cs a cualquier GameObject (p. ej., el Canvas o uno vacío).
Asignar Referencias UI: Selecciona el GameObject con el script. En el Inspector:
Arrastra el GameObject PuntuacionText al campo Puntuacion Text.
Arrastra el GameObject BotonSumar al campo Boton Sumar.
Ejecutar Juego: Play. Pulsa el botón. La puntuación debería aumentar.
Detener Juego.
Ejercicio 18: Colisión + UI (Manzanas Rojas/Verdes)

Enunciado: Simula el ejemplo de las manzanas. Crea dos tipos de GameObjects (p. ej., Cube rojo y Cube verde) con colliders. Crea un script que detecte colisiones con ellos y aumente contadores internos. Muestra los contadores en UI (TextMeshPro).

Pasos:

Crear Canvas: UI → Canvas.
Añadir Textos UI:
UI → Text - TextMeshPro. Nómbralo TextoManzanasRojas. Cambia el texto a "Manzanas Rojas: 0".
UI → Text - TextMeshPro. Nómbralo TextoManzanasVerdes. Cambia el texto a "Manzanas Verdes: 0".
UI → Text - TextMeshPro. Nómbralo TextoTotal. Cambia el texto a "Total: 0".
Crear GameObjects "Manzanas":
3D Object → Cube. Nómbralo ManzanaRoja.
3D Object → Cube. Nómbralo ManzanaVerde.
Añade tags: Selecciona ManzanaRoja, en el Inspector, arriba, hay una casilla Tag. Crea un nuevo tag llamado "Roja" y asígnalo. Haz lo mismo con ManzanaVerde, crea y asigna el tag "Verde".
Crear GameObject "Jugador": 3D Object → Capsule. Nómbralo Jugador. Añade un Rigidbody (Add Component → Physics → Rigidbody). Añade un Collider si no lo tiene (Add Component → Physics → Capsule Collider).
Crear Script: Scripts → Create → MonoBehaviour Script → RecolectorManzanas
Editar Script:
using UnityEngine;
using TMPro; // Importar TextMeshPro

public class RecolectorManzanas : MonoBehaviour
{
    public TextMeshProUGUI textoRojas;
    public TextMeshProUGUI textoVerdes;
    public TextMeshProUGUI textoTotal;

    private int manzanasRojas = 0;
    private int manzanasVerdes = 0;

    void UpdateUI()
    {
        textoRojas.text = "Manzanas Rojas: " + manzanasRojas;
        textoVerdes.text = "Manzanas Verdes: " + manzanasVerdes;
        textoTotal.text = "Total: " + (manzanasRojas + manzanasVerdes);
    }

    void OnCollisionEnter(Collision other)
    {
        if (other.gameObject.CompareTag("Roja"))
        {
            manzanasRojas++;
            Destroy(other.gameObject); // Elimina la manzana roja recolectada
            UpdateUI(); // Actualiza la UI
        }
        else if (other.gameObject.CompareTag("Verde"))
        {
            manzanasVerdes++;
            Destroy(other.gameObject); // Elimina la manzana verde recolectada
            UpdateUI(); // Actualiza la UI
        }
    }
}
Guardar y Volver a Unity.
Adjuntar Script: Adjunta RecolectorManzanas.cs al GameObject Jugador.
Asignar Referencias UI: Selecciona Jugador. En el Inspector, arrastra los GameObjects de texto (TextoManzanasRojas, TextoManzanasVerdes, TextoTotal) a sus respectivos campos en el script.
Posicionar GameObjects: Coloca Jugador, ManzanaRoja y ManzanaVerde en la escena para que puedan colisionar.
Ejecutar Juego: Play. Mueve el Jugador para que choque con las manzanas. La UI debería actualizar los contadores.
Detener Juego.
Ejercicio 19: PlayerPrefs - Guardar Puntuación

Enunciado: Modifica el ejemplo anterior para guardar la puntuación total más alta en PlayerPrefs y mostrarla en la UI.

Pasos:

Modificar Script RecolectorManzanas: Añade una referencia a un nuevo texto para la puntuación más alta y lógica para manejarla.
using UnityEngine;
using TMPro; // Importar TextMeshPro
using UnityEngine.SceneManagement; // Importar para reiniciar escena (opcional)

public class RecolectorManzanas : MonoBehaviour
{
    public TextMeshProUGUI textoRojas;
    public TextMeshProUGUI textoVerdes;
    public TextMeshProUGUI textoTotal;
    public TextMeshProUGUI textoRecord; // Nueva referencia

    private int manzanasRojas = 0;
    private int manzanasVerdes = 0;
    private int recordActual = 0; // Variable interna para el récord actual

    void Start()
    {
        // Cargar récord al iniciar la escena
        recordActual = PlayerPrefs.GetInt("MejorPuntuacion", 0); // Valor por defecto 0 si no existe
        textoRecord.text = "Récord: " + recordActual;
    }

    void UpdateUI()
    {
        textoRojas.text = "Manzanas Rojas: " + manzanasRojas;
        textoVerdes.text = "Manzanas Verdes: " + manzanasVerdes;
        textoTotal.text = "Total: " + (manzanasRojas + manzanasVerdes);

        int totalActual = manzanasRojas + manzanasVerdes;
        if (totalActual > recordActual)
        {
            recordActual = totalActual;
            textoRecord.text = "Récord: " + recordActual;
            PlayerPrefs.SetInt("MejorPuntuacion", recordActual); // Guardar nuevo récord
            PlayerPrefs.Save(); // Asegura que se guarde en disco
        }
    }

    void OnCollisionEnter(Collision other)
    {
        if (other.gameObject.CompareTag("Roja"))
        {
            manzanasRojas++;
            Destroy(other.gameObject);
            UpdateUI();
        }
        else if (other.gameObject.CompareTag("Verde"))
        {
            manzanasVerdes++;
            Destroy(other.gameObject);
            UpdateUI();
        }
    }

    // Opcional: Función para reiniciar la escena y probar el récord
    // void Update()
    // {
    //     if (Input.GetKeyDown(KeyCode.R))
    //     {
    //         SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    //     }
    // }
}
Guardar y Volver a Unity.
Añadir Texto para Récord: UI → Text - TextMeshPro. Nómbralo TextoRecord.
Asignar Nueva Referencia: En el Inspector del Jugador, arrastra TextoRecord al nuevo campo Texto Record del script.
Ejecutar Juego: Recoge manzanas. Cierra y vuelve a abrir el juego. El récord debería persistir.
Detener Juego.

Más Ejercicios Kotlin
Ejercicio 17: Función que recibe una lista y devuelve otra transformada

Enunciado: Escribe una función duplicarElementos que reciba una List<Int> y devuelva una nueva List<Int> donde cada número esté duplicado.

Solución:
fun duplicarElementos(numeros: List<Int>): List<Int> {
    return numeros.map { it * 2 }
}

fun main() {
    val entrada = listOf(1, 2, 3, 4, 5)
    val salida = duplicarElementos(entrada)
    println("Entrada: $entrada")
    println("Salida: $salida")
}

Ejercicio 18: Función con when y tipos

Enunciado: Escribe una función procesarEntrada que reciba un Any y devuelva un String indicando el tipo y su valor (p. ej., "Es un Int: 5", "Es un String: Hola", "Tipo desconocido"). Usa when con is.

Solución:
fun procesarEntrada(entrada: Any): String {
    return when (entrada) {
        is Int -> "Es un Int: $entrada"
        is String -> "Es un String: $entrada"
        is Double -> "Es un Double: $entrada"
        else -> "Tipo desconocido: ${entrada::class.simpleName}"
    }
}

fun main() {
    println(procesarEntrada(42))
    println(procesarEntrada("Kotlin"))
    println(procesarEntrada(3.14))
    println(procesarEntrada(true))
}

Ejercicio 19: Data Class con copy y componentN

Enunciado: Define una data class Punto con x e y. Crea una instancia. Usa copy para crear una nueva instancia cambiando solo x. Usa componentN para desestructurar la primera instancia en variables.

Solución:
data class Punto(val x: Int, val y: Int)

fun main() {
    val punto1 = Punto(10, 20)

    // Usar copy para cambiar solo x
    val punto2 = punto1.copy(x = 30)

    // Desestructurar punto1
    val (x1, y1) = punto1 // Equivalente a val x1 = punto1.component1(); val y1 = punto1.component2();

    println("Punto 1: $punto1")
    println("Punto 2 (x cambiado): $punto2")
    println("Coordenadas de Punto 1: x=$x1, y=$y1")
}

Ejercicio 20: Clase Abstracta y Herencia (Similar al ejemplo anterior, pero más complejo)

Enunciado: Define una clase abstracta Forma con propiedades color y un método abstracto area(). Crea clases Circulo (radio) y Rectangulo (base, altura) que hereden de Forma. Crea una lista de Forma y calcula el área total.

Solución:
abstract class Forma(val color: String) {
    abstract fun area(): Double
}

class Circulo(color: String, val radio: Double) : Forma(color) {
    override fun area(): Double {
        return Math.PI * radio * radio
    }
}

class Rectangulo(color: String, val base: Double, val altura: Double) : Forma(color) {
    override fun area(): Double {
        return base * altura
    }
}

fun main() {
    val formas: List<Forma> = listOf(
        Circulo("Rojo", 2.0),
        Rectangulo("Azul", 3.0, 4.0),
        Circulo("Verde", 1.0),
        Rectangulo("Amarillo", 5.0, 2.0)
    )

    var areaTotal = 0.0
    for (forma in formas) {
        areaTotal += forma.area()
    }

    println("Área total de todas las formas: $areaTotal")
}

Ejercicio 21: Uso de let, run, apply, also

Enunciado: Dado un objeto Persona (nombre, edad), usa apply para inicializarlo parcialmente, let para operar si no es nulo, run para calcular algo condicionalmente, y also para registrar una acción.

Solución:
data class Persona(var nombre: String, var edad: Int)

fun main() {
    var persona: Persona? = null

    // apply: útil para inicializar
    persona = Persona(nombre = "Ana", edad = 0).apply {
        edad = 25 // Configura edad
    }

    // let: útil para operar si no es nulo
    persona?.let { p ->
        println("Nombre: ${p.nombre}")
    }

    // run: útil para calcular un valor condicionalmente
    val descripcion = persona?.run {
        if (edad >= 18) "Mayor de edad" else "Menor de edad"
    } ?: "Persona nula"
    println("Descripción: $descripcion")

    // also: útil para efectos secundarios
    persona?.also { p ->
        println("Procesando persona: ${p.nombre}")
    }
}
Ejercicio 22: Aplicación de Consola Interactiva (Simulación de Menú Simple con Lógica de Negocio)

Enunciado: Crea una aplicación que simule una tienda simple. El usuario puede ver una lista de productos (nombre, precio), elegir uno por índice, y añadirlo a un carrito. El carrito debe mostrar los productos añadidos y el total. Debe haber un menú principal con opciones para "Ver Productos", "Añadir al Carrito", "Ver Carrito", y "Salir".

Solución:
data class Producto(val nombre: String, val precio: Double)

data class Carrito(val items: MutableList<Producto> = mutableListOf()) {
    fun añadirProducto(producto: Producto) {
        items.add(producto)
    }

    fun calcularTotal(): Double {
        return items.sumOf { it.precio }
    }

    fun mostrarCarrito() {
        if (items.isEmpty()) {
            println("El carrito está vacío.")
            return
        }
        println("--- Carrito ---")
        items.forEachIndexed { index, producto ->
            println("$index - ${producto.nombre}: ${producto.precio}€")
        }
        println("Total: ${calcularTotal()}€")
    }
}

fun main() {
    val productos = listOf(
        Producto("Manzana Roja", 0.5),
        Producto("Manzana Verde", 0.4),
        Producto("Plátano", 0.3),
        Producto("Leche", 1.2),
        Producto("Pan", 0.8)
    )

    val carrito = Carrito()
    var opcion: String

    do {
        println("\n--- Tienda ---")
        println("1. Ver Productos")
        println("2. Añadir al Carrito")
        println("3. Ver Carrito")
        println("0. Salir")
        print("Elige una opción: ")
        opcion = readln()

        when (opcion) {
            "1" -> {
                println("--- Productos Disponibles ---")
                productos.forEachIndexed { index, producto ->
                    println("$index - ${producto.nombre}: ${producto.precio}€")
                }
            }
            "2" -> {
                println("--- Productos Disponibles ---")
                productos.forEachIndexed { index, producto ->
                    println("$index - ${producto.nombre}: ${producto.precio}€")
                }
                print("Introduce el índice del producto a añadir: ")
                val indiceStr = readln()
                val indice = indiceStr.toIntOrNull()
                if (indice != null && indice >= 0 && indice < productos.size) {
                    carrito.añadirProducto(productos[indice])
                    println("Producto '${productos[indice].nombre}' añadido al carrito.")
                } else {
                    println("Índice no válido.")
                }
            }
            "3" -> {
                carrito.mostrarCarrito()
            }
            "0" -> println("¡Gracias por su visita!")
            else -> println("Opción no válida.")
        }
    } while (opcion != "0")

    println("Aplicación finalizada.")
}

