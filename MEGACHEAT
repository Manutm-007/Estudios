# Mega CHEAT para Examen de PMDM (Uds 1-5) - Ejercicios Resueltos

## Índice

1. [Introducción a Videojuegos y Unity (UD1, UD2)](#unidad-1-y-2---introducción-a-videojuegos-y-unity)
2. [Gestión y Programación en Unity (UD3)](#unidad-3---gestión-y-programación-en-unity)
3. [Introducción a la Programación Móvil (UD4)](#unidad-4---introducción-a-la-programación-móvil)
4. [Fundamentos de Kotlin (UD5)](#unidad-5---fundamentos-de-kotlin)
5. [Ejercicios Prácticos Unity - Paso a Paso desde Cero](#ejercicios-prácticos-unity---paso-a-paso-desde-cero)
6. [Ejercicios Prácticos Kotlin - Paso a Paso desde Cero](#ejercicios-prácticos-kotlin---paso-a-paso-desde-cero)
7. [Más Ejercicios Unity y Kotlin](#más-ejercicios-unity-y-kotlin)

---

## Unidad 1 y 2 - Introducción a Videojuegos y Unity

### ¿Qué es Unity?

*   **Definición:** Motor de videojuegos **multiplataforma**.
*   **Origen:** 2005.
*   **Características:**
    *   Permite desarrollo de **juegos 2D y 3D**.
    *   Soporta desarrollo para ~20 plataformas (PC, iOS, Android).
    *   Ofrece un conjunto de herramientas completo, minimiza necesidad de herramientas externas.
    *   Utiliza **Programación Orientada a Objetos**.
    *   El motor está basado en una **jerarquía de GameObjects**.

### Unity Hub

*   **Función:** Gestionar **versiones** del editor de Unity.
*   **Requisito:** Necesita un **Unity ID** para su uso.
*   **Funcionalidades:**
    *   Gestionar proyectos.
    *   Acceder a la **Unity Asset Store** (assets gratuitos y de pago).
    *   Instalar/editar versiones del editor.

### Instalación de Unity

*   **Componente Necesario:** Editor de Unity.
*   **Configuración Inicial:**
    *   Seleccionar **plataformas** objetivo (PC, Android, iOS, etc.).
    *   Elegir **módulos** para compilación, idiomas, documentación.
    *   Elegir **editor de código** (Visual Studio Community, Visual Studio Code, u otros).
*   **LTS vs Recomendada:** LTS (Long Term Support) para estabilidad, versión más reciente para novedades. El curso usa la versión más reciente (6.2).
*   **IL2CPP:** Librería que convierte scripts C# a C++ para compilar nativamente en la plataforma destino (especialmente en Linux Build Support).

### Crear Proyecto Unity

*   **Acceso:** Desde **Unity Hub** -> Sección Projects -> Botón New Project.
*   **Plantillas:** Seleccionar tipo de proyecto (Universal 3D, 2D, etc.) para cargar librerías adecuadas.
*   **Ubicación:** Elegir nombre y carpeta de guardado.
*   **Resultado:** El proyecto se crea y queda disponible en Unity Hub. Se abre automáticamente en el Editor.

### Editor de Unity - Interfaz y Conceptos Básicos

*   **Scenes:** Representan las "pantallas" del juego. Contienen GameObjects.
*   **GameObject:** Elementos básicos del juego (cámara, luz, modelos, scripts, UI).
*   **Hierarchy:** Muestra todos los GameObjects de la **Scene actual**. Tiene estructura jerárquica.
*   **Scene View:** Vista 3D/2D de la escena actual.
*   **Inspector:** Muestra las propiedades y componentes del GameObject seleccionado.
*   **Project Manager (Assets):** Gestiona archivos del proyecto (scripts, materiales, modelos, etc.).
*   **Game View:** Vista de la cámara del juego durante la reproducción.

### Componentes Básicos de un Nuevo Proyecto

*   **Main Camera:** GameObject de tipo Cámara.
*   **Directional Light:** GameObject de tipo Luz direccional.
*   **Global Volume:** GameObject para efectos de postprocesado.

### Ejecución del Juego ("Play Mode")

*   **Botón:** ▶ en la barra superior del editor.
*   **Cambio de Vista:** La Scene View cambia a la vista de la cámara activa (Game View).
*   **Modo Oscuro:** Interfaz se oscurece.
*   **Valores Temporales:** Los cambios hechos durante la ejecución se pierden al detenerse, a menos que se guarden explícitamente.
*   **Playmode Tint:** Se puede cambiar el color de superposición en `Menu → Edit → Preferences → Colors` para distinguir fácilmente si el juego está corriendo.

### Scripts en Unity

*   **Lenguaje:** **C#** es el único lenguaje recomendado actualmente.
*   **Definición:** Archivos de código que definen la funcionalidad del juego.
*   **Creación:** `Project Manager -> Click Derecho -> Create -> MonoBehaviour Script`.
*   **Ubicación Recomendada:** Crear carpeta `Scripts` dentro de `Assets`.
*   **Nomenclatura:** CamelCase con primera letra mayúscula (ej. `MyScript.cs`).
*   **Clase Base:** `MonoBehaviour`. Heredar de esta clase es obligatorio para scripts adjuntos a GameObjects.
*   **Adjuntar a GameObject:** Arrastrar el script desde el Project Manager al GameObject en la Hierarchy o al Inspector del GameObject.
*   **Componente:** Al adjuntar, el script se convierte en un componente del GameObject y aparece en su Inspector.

### Estructura Básica de un Script Unity

```csharp
using System.Collections; // Bibliotecas necesarias
using System.Collections.Generic;
using UnityEngine; // Biblioteca principal de Unity

public class NombreScript : MonoBehaviour // Nombre de la clase coincide con el archivo, hereda de MonoBehaviour
{
    // Variables públicas aparecen en el Inspector
    public int vida = 100;
    // Variables privadas no aparecen en el Inspector
    private float velocidad = 5.0f;

    // Start se llama antes del primer frame update, después de que el objeto esté activo
    void Start()
    {
        Debug.Log("El juego ha comenzado!");
    }

    // Update se llama una vez por frame
    void Update()
    {
        // Código que se repite cada frame (movimiento, input, etc.)
    }

    // Otros métodos de ciclo de vida comunes
    void Awake() // Se llama cuando el script se carga, antes de Start. Útil para inicializaciones tempranas.
    {
        // Ejemplo: DontDestroyOnLoad(this); // Mantiene el GameObject entre escenas
    }

    void FixedUpdate() // Se llama a intervalos fijos, ideal para física.
    {
        // Código relacionado con física (Rigidbody)
    }

    void OnEnable() // Se llama cuando el script se habilita (GameObject activado o script activado)
    {
        Debug.Log("Script habilitado");
    }

    void OnDisable() // Se llama cuando el script se deshabilita
    {
        Debug.Log("Script deshabilitado");
    }
}
Tipos de Datos en C# (para Unity)
Básicos:
int: Números enteros (ej. 5, -10).
float: Números decimales (ej. 3.14f, 2.5f). Importante la 'f'.
double: Números decimales de doble precisión (menos común en Unity).
bool: Booleano, true o false.
char: Un solo carácter (ej. 'A', '7').
string: Cadena de caracteres (ej. "Hola Mundo").
Específicos de Unity:
Vector2: Representa 2D (x, y).
Vector3: Representa 3D (x, y, z). Muy común para posiciones, rotaciones, escalas, direcciones.
Vector4: Representa 4D (x, y, z, w).
Quaternion: Representa rotaciones (usado internamente por Transform.rotation).
Color: Representa colores (r, g, b, a).
GameObject: Referencia a un GameObject.
Component: Clase base de todos los componentes (Collider, Renderer, etc.).
Rigidbody: Componente para física.
Collider: Componente para detección de colisiones.
Transform: Componente que define posición, rotación y escala.
Operadores en C#
Aritméticos: +, -, *, /, % (módulo).
Comparación: ==, !=, <, >, <=, >=.
Lógicos: && (AND), || (OR), ! (NOT).
Asignación: =, +=, -=, *=, /=.
Clase Mathf (Operaciones Matemáticas)
Propósito: Contiene métodos para operaciones matemáticas comunes con float.
Ejemplos:
Mathf.Sin(angle), Mathf.Cos(angle), Mathf.Tan(angle).
Mathf.Abs(value): Valor absoluto.
Mathf.Sqrt(value): Raíz cuadrada.
Mathf.Pow(f, p): f elevado a p.
Mathf.Min(a, b), Mathf.Max(a, b): Mínimo/máximo.
Mathf.Clamp(value, min, max): Limita un valor entre min y max.
Mathf.Round(value): Redondea al entero más cercano.
Mathf.PI: Constante Pi.
Variables en C#
Declaración: tipo nombre; (ej. int edad;).
Inicialización: tipo nombre = valor; (ej. int edad = 25;).
Modificadores de Acceso (en propiedades de clase):
public: Visible en el Inspector y desde otros scripts.
private: Visible solo dentro de la clase del script (recomendado por defecto).
[SerializeField]: Hace que una variable private sea visible en el Inspector sin ser public.
Cambio de Valor: nombre = nuevoValor; (ej. edad = 26;).
Estructuras de Control
if, else if, else:
if (condición) {
    // código si condición es true
} else if (otraCondición) {
    // código si otraCondición es true
} else {
    // código si ninguna condición anterior es true
}
switch:
switch (variable) {
    case valor1:
        // código
        break;
    case valor2:
        // código
        break;
    default:
        // código si no coincide con ningún caso
        break;
}
while:
while (condición) {
    // código que se repite mientras condición sea true
}
do-while:
do {
    // código que se ejecuta al menos una vez
} while (condición);
for:
for (int i = 0; i < limite; i++) {
    // código que se repite, usando i como contador
}
foreach:
foreach (Tipo item in coleccion) {
    // código que se repite para cada item en la coleccion
}
Arrays
Declaración con tamaño:
int[] numeros = new int[5]; // Array de 5 enteros
numeros[0] = 10; // Asignar valor a índice 0
Declaración con valores iniciales:
string[] nombres = {"Ana", "Luis", "Marta"};
Longitud: array.Length.
Recorrido con for:
for (int i = 0; i < nombres.Length; i++) {
    Debug.Log(nombres[i]);
}
Recorrido con foreach:
foreach (string nombre in nombres) {
    Debug.Log(nombre);
}
Listas (List<T>)
Importar: using System.Collections.Generic;
Declaración vacía:
List<int> listaNumeros = new List<int>();
Declaración con valores:
List<string> listaNombres = new List<string> {"Juan", "Sofia"};
Operaciones:
lista.Add(elemento): Añadir elemento al final.
lista.Remove(elemento): Eliminar primera aparición de un elemento.
lista.RemoveAt(indice): Eliminar elemento en un índice específico.
lista.Count: Obtener cantidad de elementos.
lista.Clear(): Eliminar todos los elementos.
lista.Contains(elemento): Verificar si contiene un elemento.
lista.Sort(): Ordenar (si el tipo lo permite).
lista[0]: Acceder/Modificar elemento por índice.
ArrayList (No recomendado, usar List<T>)
Característica: Puede almacenar datos de diferentes tipos.
Riesgo: No hay comprobación de tipos en tiempo de compilación.
Reemplazo: List<T> es más seguro y eficiente.
HashTable (No recomendado, usar Dictionary<TKey, TValue>)
Característica: Colección de pares clave-valor.
Clave: Siempre de tipo string.
Tamaño: Dinámico.
Reemplazo: Dictionary<TKey, TValue> es más seguro y eficiente.
Métodos en C#
Declaración:
[acceso] tipoRetorno nombreMetodo([parametros]) {
    // cuerpo del método
    // return valor; // si tipoRetorno no es void
}
Ejemplo:
public int Sumar(int a, int b) {
    return a + b;
}
Llamada:
int resultado = Sumar(5, 3);
Game Loop en Unity
Definición: Ciclo de vida de un script durante la ejecución del juego.
Fases y Métodos Asociados:
Awake: Se llama cuando se carga el script (una vez, antes de Start). Ideal para inicializaciones tempranas y establecer referencias.
OnEnable: Se llama cuando el script se habilita.
Start: Se llama antes del primer Update. Ideal para inicializaciones que dependen de otros objetos ya inicializados.
FixedUpdate: Se llama a intervalos fijos. Ideal para física y Rigidbody.
Update: Se llama una vez por frame. Ideal para lógica de juego, input, movimiento no físico.
LateUpdate: Se llama después de todos los Update. Útil para movimiento de cámara que sigue un objeto.
OnDisable: Se llama cuando el script se deshabilita.
OnDestroy: Se llama cuando el GameObject se destruye.
Unidad 3 - Gestión y Programación en Unity
Scene View y Manipulación de GameObjects
Gizmos: Gráficos auxiliares que muestran información del GameObject (posición, dirección de luz, etc.).
Sistema de Coordenadas: Unity usa Y-Up (eje Y vertical, X horizontal, Z profundidad).
Scene Gizmo: En esquina superior derecha. Permite cambiar la vista de la escena (clic en ejes, cubo central).
Herramientas de Transformación:
Move (W): Mover GameObject.
Rotate (E): Rotar GameObject.
Scale (R): Escalar GameObject.
Rect Tool (T): Modificar RectTransform (UI).
Pivot: Punto de referencia desde el cual se aplican transformaciones. Por defecto está en el centro del GameObject.
Navegación Scene View (Teclado):
Alt + Botón Izquierdo: Orbitar cámara.
Alt + Botón Derecho: Zoom.
Alt + Botón Central (o Rueda) / F: Pan / Enfocar objeto seleccionado.
Navegación Scene View (Ratón):
Botón Izquierdo: Seleccionar GameObject.
Botón Derecho: Abrir menú contextual.
Rueda: Zoom.
Arrastrar con Rueda: Pan.
Añadir GameObjects: Click Derecho en Hierarchy o Menú -> GameObject -> 3D Object / UI / etc. o Ctrl + Shift + N.
Modificar GameObjects: Seleccionar y usar Inspector o herramientas de transformación (W, E, R).
Snap: Ajustar movimientos/rotaciones/escalas a valores específicos. Ctrl + Arrastrar con herramienta o Editar -> Snapping Settings.
Vertex Snap: Alinear GameObjects usando vértices. V + Arrastrar con herramienta Move.
Materiales y Texturas
Material: Define la apariencia visual de un GameObject (color, brillo, textura).
Crear Material: Click Derecho en Project Manager -> Create -> Material.
Aplicar Material: Arrastrar el material al GameObject o al componente Mesh Renderer en el Inspector.
Physic Material: Controla fricción y rebote para físicas. Click Derecho -> Create -> Physic Material.
Componentes Comunes
Transform: Posición (x, y, z), Rotación (x, y, z), Escala (x, y, z). Presente en todos los GameObjects.
Mesh Filter: Contiene la malla (forma) del GameObject 3D.
Mesh Renderer: Renderiza la malla con el material asignado.
Collider: Define el contorno físico para detección de colisiones.
Rigidbody: Componente necesario para que un GameObject esté afectado por la física (gravedad, fuerzas). No modificar Transform directamente si tiene Rigidbody.
Camera: Componente para renderizar una vista.
Light: Componente para emitir luz.
UI (Interfaz de Usuario)
Canvas: Contenedor principal para todos los elementos de UI. Todos los GameObjects de UI deben ser hijos de un Canvas.
Elementos UI comunes: Text, Image, Button, Slider, Input Field.
TextMeshPro: Versión mejorada del componente Text (recomendado). GameObject -> UI -> Text - TextMeshPro.
Sprites: Imágenes usadas para UI o 2D. Se configuran en el Inspector como Sprite (2D and UI).
Sprite Editor: Herramienta para dividir una imagen en múltiples sprites. Window -> Sprite Editor.
Prefabs
Definición: GameObjects con componentes, propiedades y jerarquía guardados como un asset reutilizable.
Crear Prefab: Arrastrar GameObject de la Hierarchy al Project Manager.
Usar Prefab: Arrastrar el asset del prefab del Project Manager a la Scene o Hierarchy.
Beneficios: Reutilización, fácil edición (cambios en prefab afectan a todas las instancias), organización.
Instanciar en Runtime: Instantiate(prefab, position, rotation).
Clase GameObject (Acceso desde Script)
gameObject (minúscula): Referencia al GameObject al que está adjunto el script.
transform: Acceso directo al componente Transform del GameObject.
GetComponent<T>(): Acceder a un componente específico del GameObject actual.
Ejemplo: Collider myCollider = GetComponent<Collider>();
Acceder a Otros GameObjects:
public GameObject otroGO; -> Asignar en Inspector arrastrando.
GameObject.Find("Nombre"); -> Buscar por nombre (lento).
GameObject.FindGameObjectWithTag("Tag"); -> Buscar por tag.
GameObject.FindGameObjectsWithTag("Tag"); -> Buscar todos con el tag (devuelve array).
[SerializeField] private GameObject otroGO; -> Asignar en Inspector (más seguro que public).
Componente Transform (Acceso y Modificación desde Script)
Acceso: transform.position, transform.rotation, transform.localScale.
Mover: transform.position = nuevaPosicion; o transform.Translate(Vector3.offset);.
Mover con Velocidad (Update): transform.position += velocidad * Time.deltaTime;.
Rotar: transform.rotation = nuevaRotacion; o transform.Rotate(Vector3.euler);.
Escalar: transform.localScale = nuevoScale;.
Time.deltaTime: Fracción de segundo desde el último frame. Usar para movimiento independiente del frame rate.
Clase Input (Captura de Entrada)
Input.GetKeyDown(KeyCode.key): True si la tecla se pulsó en este frame.
Input.GetKey(KeyCode.key): True si la tecla está actualmente pulsada.
Input.GetKeyUp(KeyCode.key): True si la tecla se soltó en este frame.
Input.GetAxis("Horizontal"), Input.GetAxis("Vertical"): Devuelve un valor entre -1 y 1 basado en teclas configuradas en Input Manager (A/D, W/S, Flechas).
Input.GetButton("Fire1"), Input.GetButtonDown("Fire1"), Input.GetButtonUp("Fire1"): Similar a teclas, pero para botones virtuales (configurables).
Input System Package: Nuevo sistema de entrada de Unity (más flexible, multi-dispositivo). Requiere configuración de Input Actions.
Movimiento
Cinemático (sin física): Modificar directamente Transform.position/rotation. Usar en Update o FixedUpdate si es necesario.
Físico (con Rigidbody): Aplicar fuerzas usando Rigidbody.AddForce() o Rigidbody.velocity. Usar en FixedUpdate.
Rigidbody.isKinematic: Si es true, el Rigidbody no se ve afectado por la física, pero puede moverse con Transform.
Colisiones
Requisito: Ambos GameObjects deben tener Collider. Uno de ellos (o ambos) debe tener Rigidbody.
OnCollisionEnter(Collision col): Se llama cuando este GameObject con Rigidbody colisiona con otro con Collider.
OnCollisionStay(Collision col): Se llama mientras este GameObject con Rigidbody está colisionando con otro.
OnCollisionExit(Collision col): Se llama cuando este GameObject con Rigidbody deja de colisionar con otro.
OnTriggerEnter(Collider other): Se llama cuando este GameObject con Collider (marcado como Is Trigger) entra en contacto con otro Collider.
OnTriggerStay(Collider other): Se llama mientras este GameObject con Collider (marcado como Is Trigger) está en contacto con otro.
OnTriggerExit(Collider other): Se llama cuando este GameObject con Collider (marcado como Is Trigger) deja de estar en contacto con otro.
Métodos Útiles
Destroy(GameObject obj): Destruye un GameObject.
Destroy(GameObject obj, float delay): Destruye un GameObject después de un tiempo en segundos.
Instantiate(Object original, Vector3 position, Quaternion rotation): Crea una instancia de un prefab o GameObject en tiempo de ejecución.
Invoke(string methodName, float time): Llama a un método después de un tiempo.
InvokeRepeating(string methodName, float time, float repeatRate): Llama a un método después de un tiempo y luego repitiéndolo cada repeatRate.
CancelInvoke(): Cancela todas las invocaciones.
CancelInvoke(string methodName): Cancela invocaciones específicas.
CharacterController
Propósito: Componente para movimiento de personajes (especialmente en 1ra/3ra persona) que no se ajusta estrictamente a la física (puede cambiar de dirección instantáneamente).
Componente Asociado: Tiene un Collider cápsula integrado.
CharacterController.Move(Vector3 motion): Mueve el personaje. motion es relativo al mundo. No se ve afectado por física externa.
CharacterController.SimpleMove(Vector3 speed): Mueve el personaje. speed ya incluye Time.deltaTime. Se ve afectado por pendientes.
CharacterController.isGrounded: Booleano que indica si el personaje está tocando el suelo.
CharacterController.height, CharacterController.radius: Controlan las dimensiones del collider cápsula.
Raycast
Propósito: Lanzar un "rayo" imaginario para detectar objetos en su trayectoria.
Physics.Raycast(Ray ray, out RaycastHit hit): Lanza un rayo y devuelve información si impacta.
RaycastHit: Contiene información sobre el impacto (objeto golpeado, punto, distancia).
Ray ray = new Ray(origin, direction);: Define el rayo (origen y dirección).
Debug.DrawRay(ray.origin, ray.direction * distance, color): Dibuja visualmente el rayo en la Scene View para depuración.
Usos Comunes: Detectar clics en objetos, detectar suelo, detectar obstáculos, disparos.
Otros casts: SphereCast, BoxCast, CapsuleCast.
Navegación (NavMesh)
Propósito: Permitir que NPCs se muevan por escenas de forma inteligente (evitando obstáculos).
Componentes Clave:
NavMeshSurface: Componente que define áreas navegables (suelo, plataformas). Se "bakea".
NavMeshAgent: Componente que tiene el NPC. Le da inteligencia para moverse.
NavMeshObstacle: Componente para objetos móviles que bloquean el camino.
agent.destination = targetPosition;: Establece el destino para el agente de navegación.
Cambio de Escenas
using UnityEngine.SceneManagement;: Importar el espacio de nombres.
SceneManager.LoadScene("SceneName"): Carga una escena por nombre.
SceneManager.LoadScene(index): Carga una escena por índice (índice en Build Settings).
DontDestroyOnLoad(gameObject): Mantiene un GameObject (y sus scripts) entre escenas.
PlayerPrefs
Propósito: Almacenar datos persistentes (guardar puntuación, opciones, etc.) en el disco local del usuario.
Métodos:
PlayerPrefs.SetInt("key", value), PlayerPrefs.SetFloat("key", value), PlayerPrefs.SetString("key", value).
PlayerPrefs.GetInt("key", defaultValue), PlayerPrefs.GetFloat("key", defaultValue), PlayerPrefs.GetString("key", defaultValue).
PlayerPrefs.HasKey("key"): Verificar si existe una clave.
PlayerPrefs.DeleteKey("key"): Eliminar una clave.
PlayerPrefs.DeleteAll(): Eliminar todas las claves (¡cuidado!).
Unidad 4 - Introducción a la Programación Móvil
Características del Mundo Móvil
Dominancia: El móvil superó al PC como dispositivo principal de acceso a Internet.
Plataformas Principales: Android (Google, código abierto, más diversidad de dispositivos) e iOS (Apple, más control, actualizaciones unificadas).
Nativos Digitales: Generación que creció con la tecnología móvil.
Comparación Android vs iOS
CARACTERISTICA                ANDROID                                      IOS
Personalización               Alta, requiere conocimiento                  Menor, más controlada
Actualizaciones               Dependen del fabricante/modelo               Acceso a la última versión, automáticas
Dispositivos                  Varios fabricantes (Samsung, Google, etc.)   Solo Apple (iPhone, iPad, etc.)
Distribución de Apps          Abierta (Google Play Store, otros)           Cerrada (App Store)
Tipos de Aplicaciones Móviles
Nativas:
Ventajas: Rendimiento, integración con hardware, experiencia de usuario óptima, acceso sin conexión.
Desventajas: Incompatibilidad entre plataformas, desarrollo separado por SO, desafíos de compatibilidad de versiones.
Multiplataforma:
Ventajas: Reutilización de código, menor inversión, consistencia UI/UX, un solo equipo puede mantenerlo.
Desventajas: Rendimiento menor, menor integración con hardware, limitaciones de UI nativa.
Características de Android
Origen: Compañía Android Inc., fundada en 2003, comprada por Google en 2005.
Sistema Base: Basado en Linux.
Máquina Virtual: ART (Android Runtime) desde KitKat (4.4), compila a código nativo (AOT) para mejor rendimiento. Antes usaba Dalvik (JIT).
Formato de Aplicación: AAB (Android App Bundle) actualmente, antes APK.
Bibliotecas: OpenGL, WebKit, SQLite, etc.
Dispositivos: Smartphones, tablets, wearables (Wear OS), TV (Android TV), automóviles (Android Auto).
Retos: Fragmentación de dispositivos (hardware, pantalla, densidad), fragmentación de versiones del SO.
Fragmentación de Android
Definición: Coexistencia de muchas versiones del sistema operativo en el mercado.
Relación Versión API: Cada versión de Android tiene un nivel de API (API Level) asociado.
minSdkVersion: Versión mínima del SO requerida para que la app funcione.
targetSdkVersion: Versión del SO en la que la app está optimizada.
Librerías de Soporte: Permiten usar funciones modernas en dispositivos antiguos.
Android Studio
IDE Oficial: Entorno de desarrollo para aplicaciones Android.
Lenguajes Soportados: Java y Kotlin (recomendado).
Características: Control de versiones, emulador integrado, herramientas de debugging, integración con Google Services.
SDK: Incluye APIs, herramientas de compilación, emulador (AVD).
Emulador de Android (AVD)
Propósito: Simular dispositivos Android virtuales para pruebas.
Configuración: Se puede elegir modelo de dispositivo, versión de Android (API Level), hardware (RAM, SD).
Gestión: A través de AVD Manager en Android Studio.
Alternativas: Emuladores de terceros (BlueStacks, Genymotion).
Pruebas en Dispositivos Reales
Requisitos:
Habilitar Opciones de Desarrollador (tocar "Número de compilación" 7 veces en "Acerca del teléfono").
Habilitar Depuración USB en Opciones de Desarrollador.
Instalar drivers USB (del fabricante o de Google).
Ventaja: Probar en hardware real, con sus limitaciones y características específicas.
Unidad 5 - Fundamentos de Kotlin
Introducción a Kotlin
Relación con Android: Google lo designó como lenguaje oficial para Android en 2017, equiparándolo con Java.
Características Clave:
Interoperable con Java: Puede usar código y librerías Java y viceversa.
Conciso: Menos código boilerplate.
Nulo-Seguro: Sistema de tipos previene NullPointerExceptions.
Funcional y Orientado a Objetos: Combina ambos paradigmas.
Soporte Oficial: Integrado en Android Studio.
Sintaxis Básica
Extensión de Archivo: .kt.
Función Principal: fun main() { ... }. No necesita estar dentro de una clase.
Punto y Coma: Opcional, no se recomienda usarlo.
Comentarios: // para línea, /* */ para bloque.
Paquete e Imports: package nombre.paquete y import nombre.paquete.Clase en la parte superior.
Tipos de Datos en Kotlin
Numéricos:
Int: 32-bit entero.
Long: 64-bit entero.
Float: 32-bit decimal.
Double: 64-bit decimal.
Short: 16-bit entero.
Byte: 8-bit entero.
Literals Numéricos: Pueden usar _ para legibilidad (1_000_000).
Carácter: Char. No se puede tratar como número. Codificación UTF-16.
Booleano: Boolean. Valores true o false.
Cadena: String. Se define con " o """ (raw string, permite saltos de línea).
Templates: $variable o ${expresion} para insertar valores en cadenas.
Arrays: Array<T>. Se crean con arrayOf() o Array(size) { lambda }.
Declaración de Variables
Mutable: var nombre: Tipo = valor o var nombre = valor (inferencia de tipo).
Inmutable (Constante): val nombre: Tipo = valor o val nombre = valor.
El valor de val no puede reasignarse, pero si es un objeto, sus propiedades internas pueden cambiar.
const val NOMBRE = valor: Constante en tiempo de compilación, debe estar en top level o en object.
Conversión de Tipos
Métodos: toInt(), toDouble(), toFloat(), toString(), etc.
Importante: readln() devuelve String. Convertir si se necesita un número.
Seguridad de Nulos (Null Safety)
Por Defecto: Las variables no pueden ser null.
Tipo Nullable: Tipo? (ej. String?).
Operador Elvis (?:): val b = a ?: valorPorDefecto. Si a es null, b toma valorPorDefecto.
Operador Safe Call (?.): objeto?.propiedad. Si objeto es null, devuelve null en lugar de lanzar excepción.
Operador de Aserción (!!): objeto!!. Aserción de que objeto no es null. Lanza NullPointerException si lo es. Usar con precaución.
Operadores
Aritméticos: +, -, *, /, %, ++, --.
Asignación: =, +=, -=, *=, /=, %=.
Comparación: ==, !=, <, >, <=, >=.
Lógicos: &&, ||, !.
Control de Flujo
if:
if (condición) {
    // código
} else if (otraCondición) {
    // código
} else {
    // código
}
Como expresión: val resultado = if (condición) valor1 else valor2. Requiere else.
when:
when (variable) {
    valor1 -> println("Es valor1")
    valor2 -> {
        println("Es valor2")
        hacerAlgo()
    }
    in 1..10 -> println("Está entre 1 y 10")
    is String -> println("Es una cadena")
    else -> println("Caso por defecto")
}
Como expresión: val resultado = when (...) { ... }. Requiere cubrir todos los casos posibles o usar else.
Bucles:
for: for (item in coleccion) { ... } o for (i in 0 until 10) { ... }.
while: while (condición) { ... }.
do-while: do { ... } while (condición).
repeat: repeat(5) { println("Iteración $it") }.
Colecciones
Inmutables (Read-Only): List, Set, Map. No se pueden modificar después de la creación.
listOf(), setOf(), mapOf().
Mutables: MutableList, MutableSet, MutableMap. Se pueden modificar.
mutableListOf(), mutableSetOf(), mutableMapOf().
Operaciones comunes: size, contains, get(index), add, remove, clear, sort, filter, map, forEach.
Funciones
Declaración: fun nombre(parametros: Tipo): TipoRetorno { cuerpo }.
Sin retorno: Unit (implícito o explícito).
Parámetros: fun saludar(nombre: String, edad: Int = 0). Valor por defecto = 0.
Parámetros con nombre: saludar(nombre = "Ana", edad = 25).
Función de Expresión (Single-line): fun suma(a: Int, b: Int): Int = a + b.
Sobrecarga: Permitida, incluso fuera de clases.
vararg: fun imprimir(vararg valores: Int). Permite número variable de argumentos.
Funciones de Extensión: fun String.esVocal() = this[0] in "aeiouAEIOU". Extiende la funcionalidad de una clase sin herencia.
Programación Orientada a Objetos (POO)
Clases: class NombreClase { ... }. Heredan de Any por defecto.
Constructores:
Primario: Parte de la declaración de la clase class Persona(val nombre: String, var edad: Int).
Secundarios: constructor(nombre: String) : this(nombre, 0).
init: Bloque de inicialización que se ejecuta tras el constructor primario.
Propiedades: var nombre: String (mutable) o val nombre: String (inmutable).
Getters y Setters: Implícitos (field es el valor interno). Pueden personalizarse.
Visibilidad: public (por defecto), private, protected, internal.
Herencia: Clase base debe ser open. Clase derivada class Hija : Padre(). Miembros sobreescritos deben ser override.
Clases Abstractas: abstract class Nombre. No se pueden instanciar. Pueden tener propiedades y métodos abstractos.
Data Classes: data class Nombre(val propiedad1: Tipo). Genera automáticamente equals, hashCode, toString, copy, componentN.
Clases Enum: enum class Nombre { VALOR1, VALOR2 }. Define un conjunto fijo de constantes.
Clases Selladas (sealed): sealed class Nombre. Jerarquía de subclases conocida en tiempo de compilación. Útil con when.
Singleton (object): object Nombre { ... }. Crea una única instancia de la clase.
Clases Anidadas (inner): inner class Nombre. Tiene acceso a las propiedades de la clase externa.
Funciones de Alcance (let, run, apply, also, with)
let: objeto.let { it -> ... }. Ejecuta bloque si objeto no es null. it es el objeto. Devuelve resultado del bloque.
apply: objeto.apply { ... }. Configura el objeto. this es el objeto. Devuelve el objeto.
run: objeto.run { ... }. Configura y ejecuta. this es el objeto. Devuelve resultado del bloque. También existe sin objeto: run { ... }.
also: objeto.also { it -> ... }. Realiza acciones adicionales. it es el objeto. Devuelve el objeto.
with: with(objeto) { ... }. Agrupa llamadas. this es el objeto. Devuelve resultado del bloque.
Funciones Lambda
Definición: { parametros -> cuerpo }. Función anónima.
Inferencia de Tipo: val lambda = { a: Int, b: Int -> a + b }.
it: Nombre implícito del parámetro si solo hay uno: { it > 0 }.
Lambda como Parámetro: fun ejecutar(accion: () -> Unit) { accion() }.
Último Parámetro Lambda: Puede ponerse fuera de los paréntesis: ejecutar { println("Hola") }.
Sintaxis de Tipo: (TipoEntrada) -> TipoSalida.
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
Más Ejercicios Unity y Kotlin
Más Ejercicios Unity
Ejercicio 4: UI - Puntuación con Botón

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
Ejercicio 5: Colisión + UI (Manzanas Rojas/Verdes)

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
Ejercicio 6: PlayerPrefs - Guardar Puntuación

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
Ejercicio 4: Función que recibe una lista y devuelve otra transformada

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
Ejercicio 5: Función con when y tipos

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
Ejercicio 6: Data Class con copy y componentN

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
Ejercicio 7: Clase Abstracta y Herencia (Similar al ejemplo anterior, pero más complejo)

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
Ejercicio 8: Uso de let, run, apply, also

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
Ejercicio 9: Aplicación de Consola Interactiva (Simulación de Menú Simple con Lógica de Negocio)

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
