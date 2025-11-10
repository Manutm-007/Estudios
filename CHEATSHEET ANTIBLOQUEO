🔑 PASO 0: ANTES DE PROGRAMAR – CONFIGURACIÓN BÁSICA
🏷️ 1. Crea los TAGS (SIEMPRE LO PRIMERO)
Ve a cualquier GameObject → Inspector → Tag → Add Tag…

Crea estos Tags (según el juego):
JUEGO              TAGS NECESARIOS
Arkanoid 2D        Ball,Paddle,Brick,Wall
Plataformas 3D     Player,Coin
Ping Pong 2D/3D    Ball,Paddle

✅ Truco: Si no sabes qué Tag poner → mira el CompareTag("XXX") en el código → ese es el Tag que debes crear. 
🎨 2. UI BÁSICA (CANVAS) – PASO A PASO
1.Haz clic derecho en Hierarchy → UI → Canvas
2.Dentro del Canvas, haz clic derecho → UI → Text (o Text - TextMeshPro si lo usas)
3.Renombra el texto: ej. ScoreText, LivesText, GameOverText
4.En tu script GameManager, tendrás algo como:
public Text scoreText;
5.Arrastra el objeto ScoreText (del Canvas) al campo scoreText en el Inspector del GameManager.
❗ ERROR COMÚN: Olvidar asignar el Text en el Inspector → el juego no da error, pero no se actualiza → ¡siempre arrastra! 

🧩 3. CÓMO ASIGNAR UN SCRIPT A UN OBJETO
Crea un nuevo C# script (Assets → Create → C# Script)
Nómbralo igual que la clase: ej. PlayerController.cs → clase public class PlayerController
Arrastra el script desde Project al GameObject en Hierarchy.
Ahora en el Inspector del GameObject, verás los campos públicos → rellénalos (ej. Ground Check, Speed, etc.)
✅ Regla de oro: 

Si el script tiene public GameObject algo; → arrastra un GameObject
Si tiene public float speed; → escribe un número
Si tiene public Text texto; → arrastra un objeto UI

🕹️ PASO 1: ARKANOID 2D – PASO A PASO
🧱 Objetos que necesitas:
OBJETO                            COMPONENTES
BALL                              CircleCollider2D,Rigidbody2D(Gravity=0, Continuous), Script Ball.cs
PADDLE                            BoxCollider2D, Script Paddle.cs
BRICK                             BoxCollider2d, Script Brick.cs , Tag=Brick
Walls (top, left, right)          BoxCollider2D, Tag=Wall
Bottom Border                     BoxCollider2D+Is Trigger = true, Script BottomBorder.cs
GameManager                       Objeto vacío con script GameManager.cs + referencias UI
🎯 Flujo del juego:
Pelota empieza pegada a la paleta.
Clic → se lanza.
Choca con bloques → desaparecen → suma progreso.
Si cae abajo → BottomBorder llama a LoseLife().
Si vidas == 0 → Game Over.

🧍 PASO 2: PLATAFORMAS 3D – PASO A PASO
OBJETO                            COMPONENTES
Player                            CharacterController, Script PlayerController.cs
GroundCheck                       Hijo del Player → posición (0, -0.9, 0)
Suelo/Plataformas                 MeshCollider o BoxCollider , Static, Layer= Ground
Coin                              SphereCollider + Is Trigger = true , Script Coin.cs , Tag= Coin
GameManager                       Objeto vacío + script + UI
🎯 Flujo:
Player se mueve con WASD.
Salta solo si toca suelo (groundCheck).
Monedas: al tocarlas, desaparecen y suman puntos.
✅ NO uses Rigidbody en el jugador → usa CharacterController. 

🏓 PASO 3: PING PONG (2D Y 3D)
Diferencias clave:
             2D                                   3D
Pelota       CircleCollider2D+Rigidbody2D         SphereCollider+Rigidbody
Movimiento   Translate()                          Rigidbody.velocity
Paletas      BoxCollider2D                        BoxCollider
Física       Manual (con direction)               Unity (con Rigidbody)
🧱 Objetos comunes:
2 Paletas: una con isPlayer = true, otra false (IA)
2 Boundary: izquierda y derecha → triggers
GameManager con puntuación

🚨 QUÉ HACER SI TE BLOQUEAS EN EL EXAMEN
❌ "No sé por dónde empezar"
➡️ Empieza por el GameManager. Siempre es un GameObject vacío con un script que tiene:
public static GameManager Instance;
void Awake() { if (Instance == null) Instance = this; }
❌ "No sé cómo hacer que algo se destruya"
➡️ Usa: Destroy(gameObject); → y asegúrate de que el objeto que lo llama tenga un OnCollisionEnter o OnTriggerEnter.

❌ "La pelota no se mueve"
➡️ En 2D: ¿Tiene Rigidbody2D? ¿Gravity Scale = 0?
➡️ En 3D: ¿Rigidbody.useGravity = false? ¿Está isKinematic = false al empezar?

❌ "El texto no se actualiza"
➡️ ¿Arrastraste el Text al campo en el Inspector?
➡️ ¿Estás usando scoreText.text = "..." y no Debug.Log?

❌ "No sé cómo detectar que la pelota se cayó"
➡️ Crea un GameObject invisible abajo → Collider + Is Trigger = true → script con OnTriggerEnter.

📝 RESUMEN FINAL – LO QUE DEBES SABER DE MEMORIA
CONCEPTO                               CODIGO CLAVE
Singleton                              public static GameManager Instance;+Awake()
Mover objeto                           transform.Translate(direction * speed * Time.deltaTime);
Rebotar                                direction = Vector2.Reflect(direction, normal);
Destruir                               Destroy(gameObject);
Detectar colisión                      OnCollisionEnter2D(Collision2D col)
Detectar trigger                       OnTriggerEnter2D(Collider2D other)
Actualizar UI                          scoreText.text = score.ToString();
Input teclado                          Input.GetAxis("Horizontal")
Input clic                             Input.GetMouseButtonDown(0)
Reiniciar pelota                       transform.position = Vector3.zero;


🎁 BONUS: PLANTILLA UNIVERSAL DE GAME MANAGER
using UnityEngine;
using UnityEngine.UI;

public class GameManager : MonoBehaviour
{
    public static GameManager Instance;
    public Text scoreText;
    public int score = 0;

    void Awake()
    {
        if (Instance == null) Instance = this;
    }

    public void AddScore(int points)
    {
        score += points;
        scoreText.text = "Score: " + score;
    }
}
✅ Copia esto SIEMPRE → luego lo adaptas. 
💡 ÚLTIMO CONSEJO
En el examen:

Crea los Tags primero
Haz el Canvas y los Textos
Empieza por el GameManager
Luego la pelota o jugador
Asigna TODO en el Inspector
No necesitas memorizar todo → necesitas saber dónde está cada cosa.
  

