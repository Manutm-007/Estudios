Unidad 1 y 2 - Introducción a Videojuegos y Unity
¿Qué es Unity?
Definición: Motor de videojuegos multiplataforma.
Origen: 2005.
Características:
Permite desarrollo de juegos 2D y 3D.
Soporta desarrollo para ~20 plataformas (PC, iOS, Android).
Ofrece un conjunto de herramientas completo, minimiza necesidad de herramientas externas.
Utiliza Programación Orientada a Objetos.
El motor está basado en una jerarquía de GameObjects.
Unity Hub
Función: Gestionar versiones del editor de Unity.
Requisito: Necesita un Unity ID para su uso.
Funcionalidades:
Gestionar proyectos.
Acceder a la Unity Asset Store (assets gratuitos y de pago).
Instalar/editar versiones del editor.
Instalación de Unity
Componente Necesario: Editor de Unity.
Configuración Inicial:
Seleccionar plataformas objetivo (PC, Android, iOS, etc.).
Elegir módulos para compilación, idiomas, documentación.
Elegir editor de código (Visual Studio Community, Visual Studio Code, u otros).
LTS vs Recomendada: LTS (Long Term Support) para estabilidad, versión más reciente para novedades. El curso usa la versión más reciente (6.2).
IL2CPP: Librería que convierte scripts C# a C++ para compilar nativamente en la plataforma destino (especialmente en Linux Build Support).
Crear Proyecto Unity
Acceso: Desde Unity Hub -> Sección Projects -> Botón New Project.
Plantillas: Seleccionar tipo de proyecto (Universal 3D, 2D, etc.) para cargar librerías adecuadas.
Ubicación: Elegir nombre y carpeta de guardado.
Resultado: El proyecto se crea y queda disponible en Unity Hub. Se abre automáticamente en el Editor.
Editor de Unity - Interfaz y Conceptos Básicos
Scenes: Representan las "pantallas" del juego. Contienen GameObjects.
GameObject: Elementos básicos del juego (cámara, luz, modelos, scripts, UI).
Hierarchy: Muestra todos los GameObjects de la Scene actual. Tiene estructura jerárquica.
Scene View: Vista 3D/2D de la escena actual.
Inspector: Muestra las propiedades y componentes del GameObject seleccionado.
Project Manager (Assets): Gestiona archivos del proyecto (scripts, materiales, modelos, etc.).
Game View: Vista de la cámara del juego durante la reproducción.
Componentes Básicos de un Nuevo Proyecto
Main Camera: GameObject de tipo Cámara.
Directional Light: GameObject de tipo Luz direccional.
Global Volume: GameObject para efectos de postprocesado.
Ejecución del Juego ("Play Mode")
Botón: ▶ en la barra superior del editor.
Cambio de Vista: La Scene View cambia a la vista de la cámara activa (Game View).
Modo Oscuro: Interfaz se oscurece.
Valores Temporales: Los cambios hechos durante la ejecución se pierden al detenerse, a menos que se guarden explícitamente.
Playmode Tint: Se puede cambiar el color de superposición en Menu → Edit → Preferences → Colors para distinguir fácilmente si el juego está corriendo.
Scripts en Unity
Lenguaje: C# es el único lenguaje recomendado actualmente.
Definición: Archivos de código que definen la funcionalidad del juego.
Creación: Project Manager -> Click Derecho -> Create -> MonoBehaviour Script.
Ubicación Recomendada: Crear carpeta Scripts dentro de Assets.
Nomenclatura: CamelCase con primera letra mayúscula (ej. MyScript.cs).
Clase Base: MonoBehaviour. Heredar de esta clase es obligatorio para scripts adjuntos a GameObjects.
Adjuntar a GameObject: Arrastrar el script desde el Project Manager al GameObject en la Hierarchy o al Inspector del GameObject.
Componente: Al adjuntar, el script se convierte en un componente del GameObject y aparece en su Inspector.
Estructura Básica de un Script Unity

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
CARACTERISTICA                      ANDROID                                          IOS
Personalización                     Alta, requiere conocimiento                      Menor, más controlada
Actualizaciones                     Dependen del fabricante/modelo                   Acceso a la última versión, automáticas
Dispositivos                        Varios fabricantes (Samsung, Google, etc.)       Solo Apple (iPhone, iPad, etc.)
Distribución de Apps                Abierta (Google Play Store, otros)               Cerrada (App Store)

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
Ejercicios Prácticos
Ejercicio Unity (Ejemplo de lo que podría pedirse)
Escribe un script en C# para Unity que haga lo siguiente:

Al pulsar la tecla 'E', el GameObject al que está adjunto el script debe rotar 90 grados en el eje Y.
Al colisionar con otro GameObject que tenga la tag "Enemy", debe imprimir "¡Enemigo detectado!" en la consola.
El script debe tener una variable pública de tipo float llamada velocidad que se use para mover el GameObject hacia adelante en el eje Z cada frame.
Solución de Ejemplo:
using UnityEngine;

public class MiScript : MonoBehaviour
{
    public float velocidad = 5.0f; // Variable pública visible en Inspector

    void Update()
    {
        // 1. Rotar 90 grados en Y al pulsar 'E'
        if (Input.GetKeyDown(KeyCode.E))
        {
            transform.Rotate(0, 90f, 0); // Rotar 90 grados en eje Y
        }

        // 3. Mover hacia adelante en Z cada frame
        transform.Translate(Vector3.forward * velocidad * Time.deltaTime);
    }

    // 2. Detectar colisión con "Enemy"
    void OnCollisionEnter(Collision other)
    {
        if (other.gameObject.CompareTag("Enemy")) // Verificar tag
        {
            Debug.Log("¡Enemigo detectado!"); // Imprimir mensaje
        }
    }
}

Ejercicio Kotlin (Ejemplo de lo que podría pedirse)
Escribe una función en Kotlin que reciba una lista de números enteros y devuelva una nueva lista con solo los números pares, elevados al cuadrado.

Solución de Ejemplo:
fun paresAlCuadrado(numeros: List<Int>): List<Int> {
    return numeros
        .filter { it % 2 == 0 } // Filtra los números pares
        .map { it * it }        // Eleva cada número par al cuadrado
}
// Ejemplo de uso:
fun main() {
    val listaOriginal = listOf(1, 2, 3, 4, 5, 6, 7, 8)
    val resultado = paresAlCuadrado(listaOriginal)
    println(resultado) // Imprime: [4, 16, 36, 64]
}

Otro Ejercicio Kotlin (Más complejo):

Define una clase Libro con propiedades titulo (String), autor (String) y anioPublicacion (Int). Crea una data class Biblioteca que contenga una MutableList<Libro>. Añade métodos para:

Añadir un libro.
Buscar libros por autor.
Eliminar un libro por título.
Solución de Ejemplo:
// Clase normal
class Libro(val titulo: String, val autor: String, val anioPublicacion: Int) {
    override fun toString(): String {
        return "\"$titulo\" de $autor ($anioPublicacion)"
    }
}

// Data class para la biblioteca
data class Biblioteca(val libros: MutableList<Libro> = mutableListOf()) {

    fun anadirLibro(libro: Libro) {
        libros.add(libro)
    }

    fun buscarPorAutor(autor: String): List<Libro> {
        return libros.filter { it.autor == autor }
    }

    fun eliminarPorTitulo(titulo: String): Boolean {
        return libros.removeIf { it.titulo == titulo } // removeIf devuelve true si se eliminó algo
    }
}

// Ejemplo de uso:
fun main() {
    val biblioteca = Biblioteca()
    biblioteca.anadirLibro(Libro("Cien años de soledad", "Gabriel García Márquez", 1967))
    biblioteca.anadirLibro(Libro("El otoño del patriarca", "Gabriel García Márquez", 1975))
    biblioteca.anadirLibro(Libro("1984", "George Orwell", 1949))

    println("Libros de Gabriel García Márquez:")
    println(biblioteca.buscarPorAutor("Gabriel García Márquez"))

    println("\nIntentando eliminar '1984':")
    println("¿Eliminado? ${biblioteca.eliminarPorTitulo("1984")}")

    println("\nContenido final de la biblioteca:")
    println(biblioteca.libros)
}
