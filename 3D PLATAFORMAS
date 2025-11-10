PlayerController.cs
// Importa las funcionalidades básicas de Unity (física, transform, entrada, etc.)
using UnityEngine;

// Clase pública que controla el movimiento del jugador en 3D
public class PlayerController : MonoBehaviour
{
    // Velocidad de movimiento horizontal del jugador (ajustable en el Inspector de Unity)
    public float moveSpeed = 6f;

    // Altura deseada del salto (no es fuerza bruta, sino altura en unidades)
    public float jumpForce = 8f;

    // Punto de control debajo del jugador para detectar si está en el suelo
    // Debe ser un GameObject hijo del jugador, ligeramente por debajo de sus pies
    public Transform groundCheck;

    // Capa (Layer) que identifica qué objetos son "suelo" (plataformas, terreno, etc.)
    public LayerMask groundLayer;

    // Radio de la esfera de detección usada para comprobar si el jugador toca el suelo
    public float groundDistance = 0.4f;

    // Referencia al componente CharacterController (más estable que Rigidbody para plataformas 3D)
    private CharacterController controller;

    // Vector que almacena la velocidad actual del jugador (incluye gravedad en Y)
    private Vector3 velocity;

    // Indica si el jugador está tocando el suelo
    private bool isGrounded;

    // Valor de gravedad (negativo porque actúa hacia abajo en el eje Y)
    private float gravity = -20f;

    // Se ejecuta una vez al inicio de la escena
    void Start()
    {
        // Obtiene el componente CharacterController adjunto al mismo GameObject que este script
        controller = GetComponent<CharacterController>();
    }

    // Se ejecuta cada frame (ideal para lectura de inputs y lógica de movimiento)
    void Update()
    {
        // Comprueba si hay objetos de la capa "groundLayer" dentro de una esfera
        // centrada en "groundCheck" con radio "groundDistance"
        isGrounded = Physics.CheckSphere(groundCheck.position, groundDistance, groundLayer);

        // Si el jugador está en el suelo y su velocidad vertical es descendente (caída)
        if (isGrounded && velocity.y < 0)
        {
            // Establece una pequeña velocidad hacia abajo para evitar "flotación"
            // y asegurar que permanece firmemente en el suelo
            velocity.y = -2f;
        }

        // Si el jugador está en el suelo y presiona la tecla de salto (espacio por defecto)
        if (isGrounded && Input.GetButtonDown("Jump"))
        {
            // Calcula la velocidad vertical necesaria para alcanzar la altura deseada
            // Fórmula física: v = √(2 * g * h) → aquí g es negativo, así que usamos -gravity
            velocity.y = Mathf.Sqrt(jumpForce * -2f * gravity);
        }

        // Lee el input horizontal (teclas A/D o flechas izq/der) → rango: -1 a 1
        float x = Input.GetAxis("Horizontal");

        // Lee el input vertical (teclas W/S o flechas arriba/abajo) → rango: -1 a 1
        float z = Input.GetAxis("Vertical");

        // Calcula la dirección de movimiento en el plano local del jugador:
        // - transform.right = dirección derecha local del jugador
        // - transform.forward = dirección adelante local del jugador
        // Esto permite que el jugador se mueva correctamente incluso si gira
        Vector3 move = transform.right * x + transform.forward * z;

        // Mueve al jugador en dirección horizontal usando CharacterController
        // Time.deltaTime hace que el movimiento sea independiente de los FPS
        controller.Move(move * moveSpeed * Time.deltaTime);

        // Aplica gravedad: aumenta la velocidad vertical hacia abajo cada frame
        velocity.y += gravity * Time.deltaTime;

        // Aplica el movimiento vertical (caída o salto) al jugador
        controller.Move(velocity * Time.deltaTime);
    }
}

Coin.cs
// Importa Unity
using UnityEngine;

// Clase para objetos recolectables (monedas, ítems, etc.)
public class Coin : MonoBehaviour
{
    // Se llama cuando otro objeto con Collider (no trigger) entra en este trigger
    // (este objeto debe tener "Is Trigger = true" en su Collider)
    void OnTriggerEnter(Collider other)
    {
        // Si el objeto que entró tiene el Tag "Player"
        if (other.CompareTag("Player"))
        {
            // Notifica al GameManager que se ha recolectado una moneda (suma puntos)
            GameManager.Instance.AddScore(10);

            // Destruye este objeto (la moneda desaparece)
            Destroy(gameObject);
        }
    }
}

// Importa Unity y el sistema de UI
using UnityEngine;
using UnityEngine.UI;

// Clase que gestiona la puntuación y otros estados globales del juego
public class GameManager : MonoBehaviour
{
    // Patrón Singleton: permite acceder a esta instancia desde cualquier script
    public static GameManager Instance;

    // Puntuación actual del jugador
    public int score = 0;

    // Referencia al componente de texto de Unity UI que muestra la puntuación
    public Text scoreText;

    // Se llama antes de Start (ideal para inicializar singletons)
    void Awake()
    {
        // Si no existe otra instancia de GameManager, esta se convierte en la única
        if (Instance == null)
        {
            Instance = this;
        }
        // (En proyectos avanzados, se destruirían duplicados, pero en examen no es necesario)
    }

    // Método público para aumentar la puntuación
    public void AddScore(int points)
    {
        // Aumenta la puntuación en la cantidad especificada
        score += points;

        // Actualiza el texto en pantalla con el nuevo valor
        scoreText.text = "Puntos: " + score;
    }
}

✅ CONFIGURACIÓN EN UNITY (¡IMPORTANTE PARA QUE FUNCIONE!)
En el Player (GameObject del jugador):
Añade el componente CharacterController (no uses Rigidbody).
Crea un hijo llamado GroundCheck:
Posición: (0, -0.9, 0) (ajusta según la altura del jugador).
Adjunta el script PlayerController.cs.
En el Inspector del script:
Arrastra el GroundCheck al campo correspondiente.
Crea una Layer llamada "Ground" y asígnala a todas las plataformas.
Selecciona esa Layer en el campo groundLayer.
Ajusta groundDistance si es necesario (0.3–0.5 suele funcionar).
En las plataformas (suelo, plataformas, etc.):
Asegúrate de que tengan MeshCollider o BoxCollider.
Marca el GameObject como Static en el Inspector (mejora el rendimiento).
Asigna la Layer "Ground".
En las monedas:
Añade un SphereCollider.
Marca "Is Trigger = true".
Asegúrate de que el jugador tenga un Collider normal (no trigger).
Adjunta el script Coin.cs.
En la UI:
Crea un Canvas con un Text (usando TextMeshPro es mejor, pero Text normal también sirve).
Arrastra ese Text al campo scoreText del GameManager.
Tags necesarios:
"Player" → en el GameObject del jugador.

 ¿POR QUÉ NO SE USA Rigidbody EN EL JUGADOR?
Rigidbody con gravedad y saltos en 3D suele causar:
Problemas al subir pendientes.
"Rebote" al aterrizar.
Dificultad para controlar la altura exacta del salto.
CharacterController está diseñado específicamente para personajes jugadores en 3D:
Maneja colisiones suaves.
Permite control preciso del salto y movimiento.
Es el estándar en juegos de plataformas 3D profesionales.
