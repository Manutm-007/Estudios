Ejercicios Prácticos Unity - Paso a Paso desde Cero
Ejercicio 1: Mi Primer Script de Movimiento (Input + Transform)
Enunciado: Crea un script que permita mover un GameObject (p. ej., un cubo) usando las teclas WASD o flechas. El movimiento debe ser suave e independiente del frame rate.

Pasos:

Abrir Unity Hub.
Crear Nuevo Proyecto: Selecciona la plantilla 3D (URP) o Universal 3D si está disponible. Asigna un nombre como Ejercicio1_TuNombre. Elige una ubicación en tu disco duro. Pulsa Create.
Esperar a que se abra el editor.
Organizar Assets: En la ventana Project (normalmente abajo), haz clic derecho en la carpeta Assets. Selecciona Create → Folder. Nómbrala Scripts.
Crear el GameObject: En la Hierarchy (normalmente arriba a la izquierda), haz clic derecho. Selecciona 3D Object → Cube. El cubo aparecerá en el centro (0,0,0).
Crear el Script: Haz clic derecho en la carpeta Scripts que acabas de crear. Selecciona Create → MonoBehaviour Script. Nómbralo MoverCubo.
Editar el Script: Haz doble clic en MoverCubo.cs. Se abrirá en tu editor de código (Visual Studio Community o Code).
Escribir el Código: Borra todo el contenido del archivo y pega este código:
using UnityEngine;

public class MoverCubo : MonoBehaviour // Nombre de la clase debe coincidir con el archivo
{
    public float velocidad = 5.0f; // Variable pública ajustable en Inspector

    void Update() // Este método se llama cada frame
    {
        // Capturar input de los ejes Horizontal y Vertical
        float movimientoX = Input.GetAxis("Horizontal"); // A/D o <- ->
        float movimientoZ = Input.GetAxis("Vertical");   // W/S o Arriba/Abajo

        // Calcular el desplazamiento
        // Time.deltaTime asegura que el movimiento sea independiente del frame rate
        Vector3 desplazamiento = new Vector3(movimientoX, 0, movimientoZ) * velocidad * Time.deltaTime;

        // Aplicar el desplazamiento a la posición actual del GameObject
        transform.Translate(desplazamiento);
    }
}
Guardar el Script: En el editor de código, pulsa Ctrl + S.
Volver a Unity.
Asociar el Script al Cubo: Selecciona el Cube en la Hierarchy. Arrastra el script MoverCubo.cs desde la ventana Project hasta el Inspector del Cube. El script aparecerá como un componente del Cube.
Ejecutar el Juego: Pulsa el botón Play (▶) en la barra superior del editor.
Probar el Movimiento: Usa las teclas W, A, S, D o las flechas para mover el cubo en la vista del juego (Game View).
Detener el Juego: Pulsa de nuevo el botón Play (▶).
Ejercicio 2: Contador de Colisiones con UI
Enunciado: Crea un jugador (esfera con Rigidbody y CharacterController no es necesario, usaremos Rigidbody para esta práctica) que colisione con otros objetos (p. ej., cubos). Cada colisión debe aumentar un contador y mostrarlo en un texto en pantalla (UI).

Pasos:

Crear Nuevo Proyecto o Abrir el Anterior.
Organizar Assets: Crea carpetas Scripts y UI.
Crear UI - Canvas y Texto:
En la Hierarchy, haz clic derecho. Selecciona UI → Canvas. Unity creará automáticamente un EventSystem.
Haz clic derecho sobre el Canvas recién creado. Selecciona UI → Text - TextMeshPro. (Puede pedirte que importes TMP Essentials, haz clic en Import). Renombra el texto a TextoContador.
En el Inspector del TextoContador, cambia el texto a Contador: 0 y ajusta el tamaño y posición si quieres.
Crear Jugador:
En la Hierarchy, haz clic derecho. Selecciona 3D Object → Sphere. Renómbrala a Jugador.
Selecciona Jugador. En el Inspector, haz clic en Add Component. Busca y añade Rigidbody.
Crear Objetos a Colisionar:
En la Hierarchy, haz clic derecho. Selecciona 3D Object → Cube. Renómbralo a Objeto1.
Duplica Objeto1 varias veces (Ctrl + D o clic derecho -> Duplicate) y colócalos alrededor de la escena.
Crear Script Contador: En la carpeta Scripts, crea un nuevo script llamado ContadorColisiones.
Editar Script Contador:
using UnityEngine;
using TMPro; // Importante para TextMeshPro

public class ContadorColisiones : MonoBehaviour
{
    public TextMeshProUGUI textoContador; // Referencia al texto UI
    private int contador = 0; // Contador interno

    void OnCollisionEnter(Collision collision)
    {
        // Verificar si colisionamos con un objeto de tipo "Cube" o con una tag específica
        // Opción 1: Por nombre (menos flexible)
        // if (collision.gameObject.name.StartsWith("Objeto")) { ... }

        // Opción 2: Por Tag (más flexible)
        if (collision.gameObject.CompareTag("Contable")) // Asegúrate de crear y asignar esta tag
        {
            contador++; // Incrementar contador
            textoContador.text = "Contador: " + contador; // Actualizar texto UI
            Destroy(collision.gameObject); // Opcional: destruir el objeto colisionado
        }
    }
}
Guardar Script.
Asignar Referencia UI: Selecciona el GameObject Jugador. Arrastra el script ContadorColisiones.cs al Inspector de Jugador. Ahora arrastra el GameObject TextoContador desde la Hierarchy hasta el campo Texto Contador que aparece en el Inspector del Jugador.
Asignar Tag: Selecciona Objeto1 y todos sus duplicados. En el Inspector, arriba, hay una casilla Tag. Haz clic en ella. Selecciona Edit Tags.... En la pestaña Tags, haz clic en el + y añade un nuevo tag llamado Contable. Selecciona Contable en la casilla de tag de Objeto1 y sus duplicados.
Ejecutar Juego: Pulsa Play. Mueve el Jugador para que colisione con los Objeto1. El contador en pantalla debería aumentar y los objetos desaparecer.
Detener Juego.
Ejercicio 3: Instanciar Prefabs con Input
Enunciado: Crea un script que, al pulsar la barra espaciadora, instancie (creé) un prefab en la posición del jugador.

Pasos:

Crear Nuevo Proyecto o Abrir el Anterior.
Organizar Assets: Carpetas Scripts, Prefabs, 3D Objects.
Crear Prefab a Instanciar:
En la Hierarchy, crea un 3D Object → Capsule. Renómbralo a ElementoPrefab.
Arrastra ElementoPrefab desde la Hierarchy hasta la carpeta Prefabs en la ventana Project. Se crea el asset ElementoPrefab.prefab. El GameObject en la escena se vuelve azul, indicando que es una instancia del prefab.
Crear Jugador (posición donde instanciar):
En la Hierarchy, crea un 3D Object → Sphere. Renómbrala a Jugador.
Crear Script de Instanciación: En la carpeta Scripts, crea un script llamado InstanciarElemento.
Editar Script:
using UnityEngine;

public class InstanciarElemento : MonoBehaviour
{
    public GameObject prefabAInstanciar; // Referencia al prefab
    public float offsetY = 1.0f; // Distancia sobre el jugador para instanciar

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space)) // Detectar pulsación de espacio
        {
            // Calcular la posición de instanciación (posición del jugador + offset)
            Vector3 posicionInstancia = transform.position + Vector3.up * offsetY;

            // Instanciar el prefab
            Instantiate(prefabAInstanciar, posicionInstancia, Quaternion.identity); // Quaternion.identity = rotación por defecto
        }
    }
}
Guardar Script.
Asignar Referencia Prefab: Selecciona el GameObject Jugador. Arrastra el script InstanciarElemento.cs al Inspector de Jugador. Arrastra el asset ElementoPrefab.prefab desde la ventana Project hasta el campo Prefab A Instanciar en el Inspector del Jugador.
Ejecutar Juego: Pulsa Play. Coloca la Main Camera en una buena posición para ver. Pulsa la barra espaciadora. Deberían aparecer nuevas cápsulas encima del jugador.
Detener Juego.






Ejercicios Prácticos Kotlin - Paso a Paso desde Cero
Ejercicio 1: Aplicación Consola Simple - Contador Manzanas
Enunciado: Crea una aplicación en Kotlin que simule una cesta de manzanas. Debe tener botones virtuales para "Añadir Manzana Roja", "Añadir Manzana Verde", "Mostrar Total" y "Salir". Usa readln() para leer la opción del usuario y when para manejarla.

Pasos:

Abrir Android Studio o tu IDE Kotlin.
Crear Nuevo Proyecto o Abrir Uno Existente: (p. ej., proyecto "Kotlin Console App").
Crear Archivo Kotlin: Haz clic derecho en el paquete (src/main/kotlin/...). New → Kotlin File/Class. Nómbralo ContadorManzanas.
Escribir Código: Pega este código en el archivo ContadorManzanas.kt:
fun main() {
    var manzanasRojas = 0
    var manzanasVerdes = 0
    var opcion: String

    println("Bienvenido al Contador de Manzanas!")

    do {
        println("\n--- Menú ---")
        println("1. Añadir Manzana Roja")
        println("2. Añadir Manzana Verde")
        println("3. Mostrar Total")
        println("0. Salir")
        print("Elige una opción: ")

        opcion = readln()

        when (opcion) {
            "1" -> {
                manzanasRojas++
                println("¡Añadida 1 Manzana Roja!")
            }
            "2" -> {
                manzanasVerdes++
                println("¡Añadida 1 Manzana Verde!")
            }
            "3" -> {
                val total = manzanasRojas + manzanasVerdes
                println("\n--- Totales ---")
                println("Manzanas Rojas: $manzanasRojas")
                println("Manzanas Verdes: $manzanasVerdes")
                println("Total de Manzanas: $total")
            }
            "0" -> println("¡Hasta luego!")
            else -> println("Opción no válida. Inténtalo de nuevo.")
        }
    } while (opcion != "0")

    println("Aplicación finalizada.")
}
Ejecutar: Haz clic derecho en el editor del archivo ContadorManzanas.kt y selecciona Run 'ContadorManzanasKt'.
Interactuar: La consola te pedirá que elijas una opción. Introduce 1, 2, 3 o 0 y pulsa Enter para interactuar con la "aplicación".
Ejercicio 2: Funciones y Listas - Filtrar y Transformar
Enunciado: Escribe una función procesarNumeros que reciba una List<Int>. La función debe devolver una nueva lista que contenga solo los números pares de la lista original, elevados al cuadrado. Usa filter y map.

Pasos:

Crear Archivo Kotlin: New → Kotlin File/Class → EjercicioListas
Escribir Código:
fun procesarNumeros(numeros: List<Int>): List<Int> {
    return numeros
        .filter { it % 2 == 0 } // Filtrar solo los pares
        .map { it * it }        // Transformar cada par elevándolo al cuadrado
}

fun main() {
    val listaEntrada = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    val listaSalida = procesarNumeros(listaEntrada)

    println("Lista original: $listaEntrada")
    println("Pares al cuadrado: $listaSalida")
}
Ejecutar y Ver Salida.
Ejercicio 3: POO Básica - Clase, Constructor, Métodos
Enunciado: Define una clase Producto con propiedades nombre (String), precio (Double), y cantidad (Int). Añade un constructor primario, métodos vender(cantidad: Int) y restaurarStock(cantidad: Int), y un toString() para mostrar la información. Crea instancias y úsalas.

Pasos:

Crear Archivo Kotlin: New → Kotlin File/Class → EjercicioPOO
Escribir Código:
class Producto(val nombre: String, val precio: Double, var cantidad: Int) {

    fun vender(cantidadAVender: Int) {
        if (cantidadAVender <= cantidad) {
            cantidad -= cantidadAVender
            println("Vendidos $cantidadAVender de '$nombre'. Stock restante: $cantidad.")
        } else {
            println("No hay suficiente stock de '$nombre'. Intento de vender: $cantidadAVender, Disponible: $cantidad.")
        }
    }

    fun restaurarStock(cantidadAAgregar: Int) {
        cantidad += cantidadAAgregar
        println("Agregados $cantidadAAgregar a '$nombre'. Stock actual: $cantidad.")
    }

    override fun toString(): String {
        return "Producto(nombre='$nombre', precio=$precio, cantidad=$cantidad)"
    }
}

fun main() {
    val producto1 = Producto("Manzana Roja", 0.5, 100)
    val producto2 = Producto("Leche", 1.2, 50)

    println(producto1)
    println(producto2)

    producto1.vender(10)
    producto2.vender(60) // Intentar vender más de lo disponible
    producto2.restaurarStock(20)

    println("\nDespués de operaciones:")
    println(producto1)
    println(producto2)
}
Ejecutar y Ver Salida.
