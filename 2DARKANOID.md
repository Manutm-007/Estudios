👉 Todos los scripts completos del proyecto Arkanoid 2D en Unity,
👉 Con un comentario en CADA LÍNEA explicando qué hace y por qué.

Codigo BASICO arkanoid 2d

Ball.cs 
// Importa las funcionalidades básicas de Unity (vectores, físicas, transform, etc.)
using UnityEngine;

// Declara una clase pública llamada Ball que hereda de MonoBehaviour (para poder adjuntarse a un GameObject en Unity)
public class Ball : MonoBehaviour
{
    // Velocidad de la pelota (puede ajustarse desde el Inspector de Unity)
    public float speed = 5f;

    // Dirección en la que se mueve la pelota (vector normalizado: longitud = 1)
    private Vector2 direction;

    // Indica si la pelota ya ha sido lanzada por el jugador (empieza en false)
    private bool isLaunched = false;

    // Se ejecuta una sola vez al inicio de la escena
    void Start()
    {
        // Al comenzar, la pelota apunta directamente hacia arriba (vector (0, 1))
        direction = Vector2.up;
    }

    // Se ejecuta cada frame (ideal para leer inputs del jugador)
    void Update()
    {
        // Si la pelota NO ha sido lanzada y el jugador hace clic (o toca en móvil)
        if (!isLaunched && Input.GetMouseButtonDown(0))
        {
            // Marca la pelota como lanzada → empieza a moverse libremente
            isLaunched = true;
        }
    }

    // Se ejecuta en intervalos fijos (ideal para movimiento físico, aunque aquí lo usamos por convención)
    void FixedUpdate()
    {
        // Si la pelota ya fue lanzada
        if (isLaunched)
        {
            // Mueve la pelota en su dirección actual, multiplicado por la velocidad y el tiempo entre frames
            // Time.fixedDeltaTime asegura movimiento suave e independiente de los FPS
            transform.Translate(direction * speed * Time.fixedDeltaTime);
        }
        else
        {
            // Si NO ha sido lanzada, la pelota sigue pegada a la paleta
            // Busca el objeto llamado "Paddle" en la escena (NO es la forma más eficiente, pero sirve para prototipos)
            GameObject paddle = GameObject.Find("Paddle");

            // Coloca la pelota en la misma posición X que la paleta, pero un poco más arriba (0.6 unidades)
            // La Z se deja en 0 porque es un juego 2D (plano XY)
            transform.position = new Vector3(
                paddle.transform.position.x,      // Misma X que la paleta
                paddle.transform.position.y + 0.6f, // Un poco más arriba
                0f                                // Z = 0 (plano 2D)
            );
        }
    }

    // Se llama automáticamente cuando este objeto colisiona con otro que tenga un Collider2D y al menos un Rigidbody2D
    void OnCollisionEnter2D(Collision2D col)
    {
        // Si el objeto con el que colisionó tiene el Tag "Paddle"
        if (col.gameObject.CompareTag("Paddle"))
        {
            // Calcula el punto de impacto relativo al centro de la paleta
            Vector2 hitPoint = (Vector2)transform.position - (Vector2)col.transform.position;

            // Normaliza la coordenada X: divide por la mitad del ancho de la paleta → resultado entre -1 (izquierda) y +1 (derecha)
            hitPoint.x /= col.collider.bounds.size.x / 2f;

            // Convierte esa posición en un ángulo de rebote (máximo ±60 grados)
            float angle = hitPoint.x * 60f;

            // Convierte el ángulo a radianes y calcula un nuevo vector de dirección usando seno (X) y coseno (Y)
            // Esto hace que la pelota rebote más horizontalmente si toca los bordes de la paleta
            direction = new Vector2(
                Mathf.Sin(angle * Mathf.Deg2Rad),   // Componente horizontal del rebote
                Mathf.Cos(angle * Mathf.Deg2Rad)    // Componente vertical (siempre positiva → hacia arriba)
            ).normalized; // Normaliza para que la velocidad no cambie por el ángulo
        }
        // Si colisiona con una pared ("Wall") o un bloque ("Brick")
        else if (col.gameObject.CompareTag("Wall") || col.gameObject.CompareTag("Brick"))
        {
            // Obtiene el primer punto de contacto de la colisión
            ContactPoint2D contact = col.GetContact(0);

            // Obtiene la normal de la superficie impactada (vector perpendicular a la superficie)
            Vector2 normal = contact.normal;

            // Calcula la nueva dirección reflejando la dirección actual sobre la normal → rebote realista
            direction = Vector2.Reflect(direction, normal);
        }
    }

    // Método público para reiniciar la pelota (llamado desde GameManager cuando se pierde una vida)
    public void ResetBall()
    {
        // Marca la pelota como no lanzada
        isLaunched = false;

        // La devuelve al centro de la pantalla (posición 0,0,0)
        transform.position = Vector3.zero;

        // Reinicia su dirección hacia arriba
        direction = Vector2.up;
    }
}

Paddle.cs
// Importa Unity Engine
using UnityEngine;

// Clase pública para controlar la paleta del jugador
public class Paddle : MonoBehaviour
{
    // Velocidad de movimiento de la paleta (ajustable en el Inspector)
    public float speed = 10f;

    // Límites izquierdo y derecho del movimiento (para que no salga de la cámara)
    public float minX = -8f, maxX = 8f;

    // Se ejecuta cada frame
    void Update()
    {
        // Intenta leer el movimiento del mouse en el eje X (útil para móviles o mouse en desktop)
        float input = Input.GetAxis("Mouse X");

        // Si no hay movimiento del mouse (ej: en teclado), usa las teclas horizontales (A/D o flechas)
        if (input == 0)
        {
            input = Input.GetAxis("Horizontal");
        }

        // Obtiene la posición actual de la paleta
        Vector3 pos = transform.position;

        // Modifica la coordenada X: input (-1 a 1) * velocidad * tiempo entre frames
        pos.x += input * speed * Time.deltaTime;

        // Limita la posición X entre minX y maxX (evita que la paleta salga de la pantalla)
        pos.x = Mathf.Clamp(pos.x, minX, maxX);

        // Aplica la nueva posición al objeto
        transform.position = pos;
    }
}

Brick.cs
// Importa Unity
using UnityEngine;

// Clase para cada bloque destructible
public class Brick : MonoBehaviour
{
    // Se llama cuando otro objeto con Rigidbody2D colisiona con este bloque
    void OnCollisionEnter2D(Collision2D col)
    {
        // Si el objeto que chocó es la pelota (tiene el Tag "Ball")
        if (col.gameObject.CompareTag("Ball"))
        {
            // Notifica al GameManager que un bloque fue destruido
            GameManager.Instance.BrickDestroyed();

            // Destruye este bloque (desaparece de la escena)
            Destroy(gameObject);
        }
    }
}

GameManager.cs
// Importa Unity y el sistema de UI
using UnityEngine;
using UnityEngine.UI;

// Clase principal que gestiona el estado del juego
public class GameManager : MonoBehaviour
{
    // Patrón Singleton: permite acceder a esta instancia desde cualquier otro script
    public static GameManager Instance;

    // Número de vidas iniciales del jugador
    public int lives = 3;

    // Cantidad total de bloques en el nivel (se calcula al inicio)
    public int totalBricks;

    // Referencia al texto de UI que muestra las vidas
    public Text livesText;

    // Paneles de Game Over y Victoria (objetos UI desactivados al inicio)
    public GameObject gameOverPanel, winPanel;

    // Referencia a la pelota (para reiniciarla)
    public Ball ball;

    // Se llama antes de Start, ideal para inicializar singletons
    void Awake()
    {
        // Si no existe otra instancia, esta se convierte en la única
        if (Instance == null)
        {
            Instance = this;
        }
        // (Opcional: destruir duplicados, pero en examen no es necesario)
    }

    // Se llama una vez al inicio
    void Start()
    {
        // Cuenta todos los GameObjects con el Tag "Brick" en la escena
        totalBricks = GameObject.FindGameObjectsWithTag("Brick").Length;

        // Actualiza el texto de vidas en pantalla
        UpdateUI();
    }

    // Método llamado por un bloque cuando es destruido
    public void BrickDestroyed()
    {
        // Reduce el contador de bloques restantes
        totalBricks--;

        // Si ya no quedan bloques
        if (totalBricks <= 0)
        {
            // Llama al método de victoria
            Win();
        }
    }

    // Método llamado cuando la pelota cae por abajo (ver BottomBorder.cs)
    public void LoseLife()
    {
        // Reduce una vida
        lives--;

        // Actualiza el texto en pantalla
        UpdateUI();

        // Si no quedan vidas
        if (lives <= 0)
        {
            // Termina el juego
            GameOver();
        }
        else
        {
            // Si aún hay vidas, reinicia la pelota
            ball.ResetBall();
        }
    }

    // Actualiza el texto de las vidas en la interfaz
    void UpdateUI()
    {
        livesText.text = "Vidas: " + lives;
    }

    // Muestra el panel de Game Over y congela el tiempo (detiene toda la lógica del juego)
    void GameOver()
    {
        gameOverPanel.SetActive(true);
        Time.timeScale = 0f; // 0 = pausa total
    }

    // Muestra el panel de Victoria y congela el tiempo
    void Win()
    {
        winPanel.SetActive(true);
        Time.timeScale = 0f;
    }
}


⚠️ ¡Este script es esencial! Sin él, no se detecta cuando la pelota se cae. 
BottomBorder.cs
// Importa Unity
using UnityEngine;

// Script para la zona inferior de la pantalla (invisible para el jugador)

    public class BottomBorder : MonoBehaviour
    {
    // Se llama cuando otro objeto entra en este trigger (debe tener "Is Trigger = true")
    void OnTriggerEnter2D(Collider2D other)
    {
        // Si el objeto que entró es la pelota
        if (other.CompareTag("Ball"))
        {
            // Notifica al GameManager que se perdió una vida
            GameManager.Instance.LoseLife();
        }
    }
    }
    
🔧 Configuración en Unity: 

Crea un GameObject vacío en la parte inferior de la pantalla.
Añádele un BoxCollider2D.
Marca "Is Trigger = true".
Adjunta este script.
Asegúrate de que la pelota tenga un Collider2D normal (no trigger).

✅ CONFIGURACIÓN FINAL EN UNITY
Tags necesarios:
"Ball" → en la pelota
"Paddle" → en la paleta
"Brick" → en todos los bloques
"Wall" → en las paredes superior/izquierda/derecha
Componentes necesarios:
Pelota: CircleCollider2D + Rigidbody2D (Gravity Scale = 0, Body Type = Dynamic, Collision Detection = Continuous)
Paleta: BoxCollider2D
Bloques: BoxCollider2D
Paredes: BoxCollider2D o EdgeCollider2D
BottomBorder: BoxCollider2D con Is Trigger = true

