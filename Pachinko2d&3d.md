🎯 ¿QUÉ ES UN PACHINKO?
Es un juego de azar típico de Japón, donde se lanza una bola desde la parte superior y rebota contra clavos, obstáculos y premios hasta caer en una ranura que da puntos o más bolas.

🛠️ REQUISITOS PREVIOS
Instalar Unity Hub (desde unity.com )
Crear un proyecto nuevo:
Para Pachinko 2D: Plantilla 2D (URP) (Universal Render Pipeline)
Para Pachinko 3D: Plantilla 3D (URP)
⚠️ Importante: Usa Unity 2022 LTS o 2023 LTS para mayor estabilidad. 

🎮 VERSIÓN 2D (PRIMERO)
📦 PASO 1: CONFIGURAR LA ESCENA
1.1. Crear objetos básicos
Cámara: Ya está.
Fondo: (Opcional) Arrastra un Sprite como fondo.
1.2. Crear el suelo y paredes
En la jerarquía: GameObject > 2D Object > Sprite > Square
Renómbralo como "ParedIzquierda"
Escala: X=0.1, Y=10
Posición: X=-5, Y=0
Haz lo mismo con "ParedDerecha" en X=5
Crea un "Suelo":
Sprite > Square
Escala: X=12, Y=0.2
Posición: Y=-6
Agrega Collider:
Con cada objeto seleccionado → Add Component > Box Collider 2D 

1.3. Añadir obstáculos (clavos)
Crea varios círculos pequeños:
GameObject > 2D Object > Circle
Escala: 0.2, 0.2, 1
Agrega Circle Collider 2D
NO le pongas Rigidbody (solo colisionan, no se mueven)
Colócalos en zig-zag entre las paredes, desde arriba hacia abajo. 

🧱 PASO 2: CREAR LA BOLA
GameObject > 2D Object > Circle
Nombre: "Bola"
Escala: 0.3, 0.3, 1
Add Component > Circle Collider 2D
Add Component > Rigidbody 2D
Gravity Scale: 3
Freeze Rotation: ✔️ (marca Z)
⚠️ Mueve la bola fuera de la escena (ej. Y=10) para que no caiga al empezar 

🔄 PASO 3: OBSTÁCULOS MÓVILES (ROTATIVOS)
Crea un círculo grande (por ejemplo, en el centro):
Escala: 0.5, 0.5, 1
Circle Collider 2D
NO Rigidbody → sí un script que lo haga rotar
Script: RotarObstaculo.cs
// Archivo: RotarObstaculo.cs
using UnityEngine;

public class RotarObstaculo : MonoBehaviour
{
    public float velocidadRotacion = 50f; // grados por segundo

    void Update()
    {
        transform.Rotate(0, 0, velocidadRotacion * Time.deltaTime);
    }
}
Arrastra este script al obstáculo móvil.
🎯 PASO 4: ZONAS DE PREMIO
Vamos a crear 2 tipos de triggers:

PremioBola: da +1 bola
PremioDinero: da +10 puntos
Crear "PremioBola"
GameObject > 2D Object > Square
Nombre: "PremioBola1"
Escala: 0.8, 0.3, 1
Posición: en el fondo (ej. Y=-5)
Color: verde (en Sprite Renderer → Material → Default → cambiar color)
Add Component > Box Collider 2D
Marca ✔️ Is Trigger
Script: PremioBola.cs
// Archivo: PremioBola.cs
using UnityEngine;

public class PremioBola : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D col)
    {
        if (col.CompareTag("Bola"))
        {
            GameManager.instance.AgregarBola();
            Destroy(col.gameObject); // destruye la bola que entró
        }
    }
}
Haz lo mismo con PremioDinero, pero con este script: 

Script: PremioDinero.cs
// Archivo: PremioDinero.cs
using UnityEngine;

public class PremioDinero : MonoBehaviour
{
    public int puntos = 10;

    private void OnTriggerEnter2D(Collider2D col)
    {
        if (col.CompareTag("Bola"))
        {
            GameManager.instance.SumarPuntos(puntos);
            Destroy(col.gameObject);
        }
    }
}
💡 Importante: Etiqueta la bola como "Bola": 

Selecciona la bola → en Inspector → Tag → Add Tag... → crea "Bola" → asígnala.
📊 PASO 5: UI (INTERFAZ)
Crear Canvas
GameObject > UI > Canvas
Dentro del Canvas:
Crea Text - TMP (TextMeshPro)
Nombre: "TextoBolas"
Texto: Bolas: 5
Posición: arriba a la izquierda
⚠️ Si no tienes TextMeshPro, haz clic en Window > TextMeshPro > Import TMP Essential Resources 

🧠 PASO 6: GAME MANAGER (EL CEREBRO DEL JUEGO)
Script: GameManager.cs
// Archivo: GameManager.cs
using UnityEngine;
using TMPro;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int bolasRestantes = 5;
    public int puntos = 0;

    public TMP_Text textoBolas;
    public GameObject prefabBola;
    public Vector2 posicionLanzamiento = new Vector2(0, 6); // arriba del todo

    void Awake()
    {
        if (instance == null)
            instance = this;
        else
            Destroy(gameObject);
    }

    void Start()
    {
        ActualizarUI();
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && bolasRestantes > 0)
        {
            LanzarBola();
        }
    }

    public void LanzarBola()
    {
        bolasRestantes--;
        Instantiate(prefabBola, posicionLanzamiento, Quaternion.identity);
        ActualizarUI();
    }

    public void AgregarBola()
    {
        bolasRestantes++;
        ActualizarUI();
    }

    public void SumarPuntos(int cantidad)
    {
        puntos += cantidad;
        ActualizarUI();
    }

    void ActualizarUI()
    {
        textoBolas.text = $"Bolas: {bolasRestantes} | Puntos: {puntos}";
    }
}
Configuración en Unity:
Crea un GameObject vacío en la escena → nombre: "GameManager"
Arrastra el script GameManager.cs a ese objeto.
En el Inspector:
Arrastra el TextoBolas al campo textoBolas
Arrastra el prefab de la bola al campo prefabBola
Para eso: arrastra la bola desde la jerarquía a la carpeta Assets, y se convierte en prefab.
Luego, arrastra esa prefab al campo.
✅ PRUEBA EL JUEGO 2D
Presiona Play
Usa ESPACIO para lanzar bolas
Si cae en verde: +1 bola
Si cae en otro color: +puntos
La UI se actualiza

🕹️ VERSIÓN 3D
La versión 3D es muy similar, pero con componentes 3D.

🧱 Diferencias clave:
CONCEPTO                   2D                                3D
Forma bola                 Circle (Sprite)                   Sphere
Collider                   CircleCollider2D                  Sphere Collider
Física                     Rigidbody2D                       Rigidbody
Obstáculos                 Sprites                           Cylinders / Capsules
Premios                    BoxCollider2D (trigger)           Box Collider (trigger)
UI                         Igual (Canvas 2D)                 Igual

🧪 PASOS RÁPIDOS PARA 3D
Escena vacía
Crea paredes con Cubos (GameObject > 3D Object > Cube)
Escala y posición como en 2D, pero en Z=0
Crea bola: Sphere
Rigidbody → Gravity ✔️
Freeze Rotation: ✔️ en X, Y, Z (para que no gire)
Crea obstáculos móviles: Cilindros o esferas
Script RotarObstaculo3D.cs:
// RotarObstaculo3D.cs
using UnityEngine;

public class RotarObstaculo3D : MonoBehaviour
{
    public float velocidad = 50f;
    void Update()
    {
        transform.Rotate(Vector3.up, velocidad * Time.deltaTime);
    }
}

Premios: usa Cubos pequeños con Box Collider → ✔️ Is Trigger
Usa mismos scripts para premios, pero con OnTriggerEnter (sin "2D"):
// PremioBola3D.cs
private void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("Bola"))
    {
        GameManager.instance.AgregarBola();
        Destroy(other.gameObject);
    }
}

GameManager: idéntico (solo cambia Instantiate(prefabBola, posicion, Quaternion.identity))
📦 RESUMEN DE ARCHIVOS DE CÓDIGO
Guarda estos 6 archivos C# en tu carpeta Assets/Scripts/:

GameManager.cs
RotarObstaculo.cs (2D)
RotarObstaculo3D.cs (3D)
PremioBola.cs
PremioDinero.cs
PremioBola3D.cs / PremioDinero3D.cs (si haces 3D)
🏁 CONSEJOS FINALES
Usa prefabs para todo lo que se repite.
Ajusta física con Physics Material (2D o 3D) para rebotes más realistas.
Si las bolas se atascan, sube la velocidad mínima en el Rigidbody.
Puedes agregar sonidos con AudioSource.

