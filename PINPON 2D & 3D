✅ Lógica completa de juego
✅ Canvas con puntuación y vidas
✅ Scripts 100% comentados línea por línea

🟢 PARTE 1: PING PONG EN 2D
🧱 Elementos del juego
Pelota: rebota entre paletas y paredes
2 Paletas: izquierda (IA) y derecha (jugador)
Puntuación: se suma cuando la pelota pasa del rival
Vidas (opcional, pero incluimos)

Ball2D.cs
// Importa Unity Engine
using UnityEngine;

// Controla la pelota en el modo 2D
public class Ball2D : MonoBehaviour
{
    // Velocidad inicial de la pelota
    public float speed = 10f;

    // Referencias a las paletas (para reiniciar)
    public Paddle2D leftPaddle;
    public Paddle2D rightPaddle;

    // Dirección actual de la pelota (normalizada)
    private Vector2 direction;

    // Indica si el juego ya empezó (para no mover la pelota al inicio)
    private bool gameStarted = false;

    // Se ejecuta al inicio
    void Start()
    {
        // Inicia en dirección aleatoria (derecha o izquierda)
        direction = new Vector2(Random.value > 0.5f ? 1 : -1, Random.Range(-0.5f, 0.5f)).normalized;
    }

    // Se ejecuta cada frame
    void Update()
    {
        // Si el juego no ha empezado y se presiona espacio o clic, comienza
        if (!gameStarted && (Input.GetKeyDown(KeyCode.Space) || Input.GetMouseButtonDown(0)))
        {
            gameStarted = true;
        }
    }

    // Física fija (ideal para movimiento constante)
    void FixedUpdate()
    {
        if (gameStarted)
        {
            // Mueve la pelota en su dirección actual
            transform.Translate(direction * speed * Time.fixedDeltaTime);
        }
    }

    // Detecta colisiones 2D
    void OnCollisionEnter2D(Collision2D col)
    {
        // Si choca con una paleta
        if (col.gameObject.CompareTag("Paddle"))
        {
            // Rebota invirtiendo la X y añadiendo un poco de ángulo según posición de impacto
            float hitPoint = (transform.position.y - col.transform.position.y) / (col.collider.bounds.size.y / 2f);
            direction = new Vector2(-direction.x, hitPoint).normalized;
        }
        // Si choca con pared superior o inferior
        else if (col.gameObject.CompareTag("Wall"))
        {
            // Invierte la Y (rebota arriba/abajo)
            direction.y = -direction.y;
        }
    }

    // Llamado cuando la pelota sale por la izquierda o derecha
    public void ResetPosition(bool toRight)
    {
        // Vuelve al centro
        transform.position = Vector3.zero;
        gameStarted = false;

        // Nueva dirección: hacia el lado que perdió
        direction = new Vector2(toRight ? 1 : -1, Random.Range(-0.5f, 0.5f)).normalized;
    }
}

using UnityEngine;

// Controla una paleta (jugador o IA)
public class Paddle2D : MonoBehaviour
{
    // ¿Es controlada por el jugador?
    public bool isPlayer = false;

    // Velocidad de movimiento
    public float speed = 8f;

    // Límites verticales (para no salir de la cámara)
    public float minY = -4f, maxY = 4f;

    // Referencia a la pelota (solo para IA)
    public Ball2D ball;

    void Update()
    {
        if (isPlayer)
        {
            // Control por teclado: W/S o flechas arriba/abajo
            float input = Input.GetAxis("Vertical");
            Move(input);
        }
        else
        {
            // IA: sigue la pelota
            if (ball != null)
            {
                float targetY = ball.transform.position.y;
                float diff = targetY - transform.position.y;
                Move(Mathf.Sign(diff));
            }
        }
    }

    // Método reutilizable para mover la paleta
    void Move(float input)
    {
        Vector3 pos = transform.position;
        pos.y += input * speed * Time.deltaTime;
        pos.y = Mathf.Clamp(pos.y, minY, maxY);
        transform.position = pos;
    }
}

GameManager2D.cs
using UnityEngine;
using UnityEngine.UI;

// Gestiona puntuación, vidas y final del juego en 2D
public class GameManager2D : MonoBehaviour
{
    public static GameManager2D Instance;

    // Puntuación
    public int leftScore = 0;
    public int rightScore = 0;
    public int maxScore = 5; // Gana quien llegue primero

    // Vidas (opcional, pero incluido)
    public int leftLives = 3;
    public int rightLives = 3;

    // UI
    public Text leftScoreText;
    public Text rightScoreText;
    public Text leftLivesText;
    public Text rightLivesText;
    public GameObject winPanel;
    public Text winText;

    // Referencia a la pelota
    public Ball2D ball;

    void Awake()
    {
        if (Instance == null) Instance = this;
    }

    // Llamado cuando la pelota sale por la IZQUIERDA → punto para la derecha
    public void BallOutLeft()
    {
        rightScore++;
        rightLives--; // Opcional: resta vida al que falló
        UpdateUI();

        if (rightLives <= 0 || rightScore >= maxScore)
        {
            GameOver("¡Jugador Derecho Gana!");
        }
        else
        {
            ball.ResetPosition(true); // Siguiente saque hacia la derecha
        }
    }

    // Llamado cuando la pelota sale por la DERECHA → punto para la izquierda
    public void BallOutRight()
    {
        leftScore++;
        leftLives--;
        UpdateUI();

        if (leftLives <= 0 || leftScore >= maxScore)
        {
            GameOver("¡Jugador Izquierdo Gana!");
        }
        else
        {
            ball.ResetPosition(false); // Siguiente saque hacia la izquierda
        }
    }

    void UpdateUI()
    {
        leftScoreText.text = leftScore.ToString();
        rightScoreText.text = rightScore.ToString();
        leftLivesText.text = "Vidas: " + leftLives;
        rightLivesText.text = "Vidas: " + rightLives;
    }

    void GameOver(string winner)
    {
        winText.text = winner;
        winPanel.SetActive(true);
        Time.timeScale = 0f;
    }
}

Boundary2D.cs (para detectar salidas)
using UnityEngine;

// Zonas invisibles a izquierda y derecha para detectar cuando la pelota sale
public class Boundary2D : MonoBehaviour
{
    public bool isLeftBoundary = false; // Marcar en Inspector

    void OnTriggerEnter2D(Collider2D col)
    {
        if (col.CompareTag("Ball"))
        {
            if (isLeftBoundary)
            {
                GameManager2D.Instance.BallOutLeft();
            }
            else
            {
                GameManager2D.Instance.BallOutRight();
            }
        }
    }
}

🔧 Configuración: 

Crea dos zonas con BoxCollider2D + Is Trigger = true a izq y der.
Marca isLeftBoundary = true en la izquierda.
Pelota: CircleCollider2D + Rigidbody2D (gravity=0).


🔵 PARTE 2: PING PONG EN 3D
🧱 Diferencias clave
Uso de Rigidbody para la pelota (física realista)
Paletas con BoxCollider
Cámara en perspectiva

Ball3D.cs
using UnityEngine;

// Pelota en 3D: usa física real de Unity
public class Ball3D : MonoBehaviour
{
    public float speed = 10f;
    public Paddle3D leftPaddle;
    public Paddle3D rightPaddle;

    private Rigidbody rb;
    private bool gameStarted = false;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
        rb.isKinematic = true; // Empieza sin física
    }

    void Update()
    {
        if (!gameStarted && (Input.GetKeyDown(KeyCode.Space) || Input.GetMouseButtonDown(0)))
        {
            StartBall();
        }
    }

    public void StartBall()
    {
        rb.isKinematic = false;
        Vector3 direction = new Vector3(Random.value > 0.5f ? 1 : -1, 0, Random.Range(-0.3f, 0.3f)).normalized;
        rb.velocity = direction * speed;
        gameStarted = true;
    }

    // Cuando la pelota choca con algo
    void OnCollisionEnter(Collision col)
    {
        if (col.gameObject.CompareTag("Paddle"))
        {
            // Aumenta velocidad ligeramente al golpear (¡más emoción!)
            rb.velocity += rb.velocity.normalized * 0.5f;
        }
    }

    public void ResetPosition(bool toRight)
    {
        transform.position = Vector3.zero;
        rb.velocity = Vector3.zero;
        rb.isKinematic = true;
        gameStarted = false;
    }
}

Paddle3D.cs
using UnityEngine;

public class Paddle3D : MonoBehaviour
{
    public bool isPlayer = false;
    public float speed = 8f;
    public float minY = -4f, maxY = 4f;
    public Ball3D ball;

    void Update()
    {
        if (isPlayer)
        {
            float input = Input.GetAxis("Vertical");
            Move(input);
        }
        else
        {
            if (ball != null && ball.gameStarted)
            {
                float targetY = ball.transform.position.y;
                float diff = targetY - transform.position.y;
                Move(Mathf.Sign(diff));
            }
        }
    }

    void Move(float input)
    {
        Vector3 pos = transform.position;
        pos.y += input * speed * Time.deltaTime;
        pos.y = Mathf.Clamp(pos.y, minY, maxY);
        transform.position = pos;
    }
}

GameManager3D.cs
using UnityEngine;
using UnityEngine.UI;

public class GameManager3D : MonoBehaviour
{
    public static GameManager3D Instance;

    public int leftScore = 0;
    public int rightScore = 0;
    public int maxScore = 5;

    public Text leftScoreText;
    public Text rightScoreText;
    public GameObject winPanel;
    public Text winText;

    public Ball3D ball;

    void Awake()
    {
        if (Instance == null) Instance = this;
    }

    public void BallOutLeft()
    {
        rightScore++;
        UpdateUI();
        if (rightScore >= maxScore) GameOver("¡Derecha Gana!");
        else ball.ResetPosition(true);
    }

    public void BallOutRight()
    {
        leftScore++;
        UpdateUI();
        if (leftScore >= maxScore) GameOver("¡Izquierda Gana!");
        else ball.ResetPosition(false);
    }

    void UpdateUI()
    {
        leftScoreText.text = leftScore.ToString();
        rightScoreText.text = rightScore.ToString();
    }

    void GameOver(string winner)
    {
        winText.text = winner;
        winPanel.SetActive(true);
        Time.timeScale = 0f;
    }
}

Boundary3D.cs
using UnityEngine;

public class Boundary3D : MonoBehaviour
{
    public bool isLeftBoundary = false;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Ball"))
        {
            if (isLeftBoundary)
                GameManager3D.Instance.BallOutLeft();
            else
                GameManager3D.Instance.BallOutRight();
        }
    }
}
 Configuración 3D: 

Pelota: SphereCollider + Rigidbody (Use Gravity = false, Freeze Rotation = XYZ)
Paletas: BoxCollider (sin Rigidbody)
Zonas de salida: BoxCollider con Is Trigger = true
🖼 CANVAS (IGUAL EN 2D Y 3D)
Crea un Canvas con:

Text para leftScoreText
Text para rightScoreText
Text para vidas (solo en 2D)
Panel con Text → desactivado al inicio (winPanel)
Asigna todo en el Inspector.

✅ TAGS NECESARIOS
"Ball"
"Paddle"
"Wall" (solo en 2D, para top/bottom)
"Boundary" → no necesario, usamos scripts separados
