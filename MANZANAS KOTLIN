Ejercicio Kotlin Propuesto: Simulación de Contador de Manzanas

Enunciado (interpretado): Escribe un programa en Kotlin que simule una aplicación simple con botones para "Añadir Manzana Roja", "Añadir Manzana Verde" y "Mostrar Total". El programa debe:

Mantener un contador para manzanas rojas y otro para manzanas verdes.
Permitir al usuario "presionar" botones virtuales para incrementar los contadores.
Mostrar el total de manzanas de cada tipo y el total general cuando se solicite.
Pasos para el Ejercicio (Simulación en Consola):

Abrir Android Studio o tu IDE Kotlin.
Crear Nuevo Proyecto o Abrir Uno Existente: (p. ej., proyecto "Hola Mundo").
Crear Archivo Kotlin: Haz clic derecho en el paquete (src/main/java/...). New → Kotlin File/Class. Nómbralo ContadorManzanas.
Escribir Código: Este código simula la interacción mediante readln() para leer la opción del usuario. Usa un bucle while para mantener la aplicación corriendo hasta que se elija salir.

import java.util.Locale

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

        opcion = readln().lowercase(Locale.getDefault())

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
Este ejemplo cubre:

Variables mutables (var): manzanasRojas, manzanasVerdes, opcion.
Control de Flujo (when, while): Para manejar las diferentes opciones del menú y mantener el programa corriendo.
Funciones (main, println, readln): Función principal y funciones de entrada/salida.
Operaciones básicas: Incremento (++) y suma (+).
Cadenas de texto (String): Para mostrar mensajes y leer la entrada del usuario.
