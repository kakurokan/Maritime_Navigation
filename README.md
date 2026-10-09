# Maritime Traffic Simulator (Simulador Marítimo)

A Java-based desktop application designed for simulating, managing, and visualizing maritime traffic in customizable environments. The simulator models ship navigation, route optimization using path finding algorithms, obstacle avoidance, and environmental dynamics like ocean currents and storms.

---

## 📌 Features

- **Maritime Navigation & Autopilot:**
  - Dynamic simulation of vessels (`Navio`, `Navegante`) moving across geometric coordinates.
  - State management for vessels (`EstadoMovel`: *Waiting*, *At Origin*, *Navigating*, *At Destination*).
  - Autopilot support for path tracking and vector computations.

- **Route Planning & Graph Routing:**
  - Route calculation using graph-based pathfinding strategies (`EstrategiaDijkstra`, `Grafo`, `Route`).
  - Strategy Pattern implementation (`EstrategiaRota`) for modular routing algorithms.

- **Obstacles & Environmental Dynamics:**
  - Geometric collision boundaries and obstacles (`Obstaculo`, `Circulo`, `Poligono`, `Retangulo`, `Quadrado`, `Triangulo`).
  - Environmental events such as ocean currents (`DialogoCorrente`) and moving storms (`Tempestade`).

- **Harbor & Control Operations:**
  - Harbor management (`Porto`) and traffic control tower (`TorreDeControlo`, `GestorMaritimo`).
  - State persistence and snapshot capture (`SnapshotSimulacao`) for tracking or replaying simulations.

- **Interactive GUI (Java Swing):**
  - Real-time 2D map visualization (`PainelMapa`, `JanelaPrincipal`).
  - Interactive simulation controls: play/pause, restart (`AcaoReiniciarSimulacao`), toggle vessel direction (`AcaoAlternarDirecao`), and configure ocean currents.

- **Comprehensive Unit Testing:**
  - Extensive test coverage for engine components, vector math, geometry, and graph routing algorithms.

---

## 🏗 Architecture & Design Patterns

The project follows a clean separation of concerns, divided into three main packages:


```

Simulador_maritimo/
├── src/
│   ├── Cliente.java                 # Entry point / Client application
│   ├── Engine/                      # Core simulation engine and business logic
│   │   ├── AutoPilot.java
│   │   ├── Circulo.java, Retangulo.java, Poligono.java, ...  # Geometric shapes & obstacles
│   │   ├── EstadoMovel.java, Movel.java, Movel*.java         # State Pattern for mobile entities
│   │   ├── EstrategiaRota.java, EstrategiaDijkstra.java     # Strategy Pattern for pathfinding
│   │   ├── GestorMaritimo.java, TorreDeControlo.java         # Traffic & harbor orchestration
│   │   ├── Grafo.java, Route.java, Ponto.java, Vetor.java   # Graph & mathematical foundations
│   │   ├── Navio.java, Navegante.java                       # Ship & navigator models
│   │   ├── Simulador.java, SnapshotSimulacao.java           # Simulation engine & snapshot manager
│   │   └── Tempestade.java                                  # Dynamic weather/storm entity
│   └── GUI/                         # Graphic User Interface (Swing)
│       ├── JanelaPrincipal.java     # Main application window
│       ├── PainelMapa.java          # 2D visual canvas for simulation rendering
│       ├── DialogoCorrente.java     # Dialog for ocean current configuration
│       └── Acao*.java               # Action handlers (Restart, Direction Toggle, etc.)
└── test/
└── Engine/                      # Unit tests for all engine components

```

### Key Design Patterns Used:
- **Strategy Pattern:** `EstrategiaRota` interface implemented by `EstrategiaDijkstra` to swap routing strategies cleanly.
- **State Pattern:** `EstadoMovel` hierarchy (`MovelNaOrigem`, `MovelNavegando`, `MovelAguardando`, `MovelNoDestino`) managing vessel lifecycle.
- **Memento / Snapshot Pattern:** `SnapshotSimulacao` for simulation state capture and playback.
- **MVC / Separation of Concerns:** Decoupled simulation logic (`Engine`) and graphical rendering (`GUI`).

---

## 🚀 Getting Started

### Prerequisites

- **Java Development Kit (JDK):** Version 8 or higher (JDK 11+ recommended).
- **IDE (Optional):** IntelliJ IDEA, Eclipse, or VS Code with Java extensions.

### Compilation & Execution

#### 1. Compile the Project
From the project root directory, compile all Java source files:

```bash
# Create output directory
mkdir -p bin

# Compile all source files
javac -d bin -sourcepath src src/Cliente.java src/Engine/*.java src/GUI/*.java

```

#### 2. Run the Application

Launch the simulator via the main entry class:

```bash
java -cp bin Cliente

```

---

## 💡 Client Usage Example

### Overview

The `Cliente` class serves as the main entry point for the Maritime Traffic Simulator. It initializes the simulation with:
- **Geometric points** representing ports and navigation waypoints
- **Routes** connecting ports across the maritime map
- **Static obstacles** (islands, shallow waters, reefs)
- **Simulation engine** with traffic control
- **Storm entities** for dynamic weather simulation
- **Traffic scheduling** with ships departing at different times

### Example: Complete Initialization with Inputs

```java
import Engine.*;
import GUI.DialogoCorrente;
import GUI.JanelaPrincipal;
import javax.swing.*;

void main() {

    // ========================================================
    // 1. DEFINE GEOGRAPHIC POINTS (Map: 19x14 units)
    // ========================================================
    
    // Main ports at cardinal positions
    Ponto pLisboa = new Ponto(1, 1);      // Southwest harbor
    Ponto pFaro = new Ponto(19, 1);       // Southeast harbor
    Ponto pVigo = new Ponto(1, 14);       // Northwest harbor
    Ponto pSagres = new Ponto(19, 14);    // Northeast harbor
    Ponto pLeixoes = new Ponto(10, 7);    // Central harbor
    
    // Navigation waypoints to create routes
    Ponto nSul1 = new Ponto(7, 1);
    Ponto nSul2 = new Ponto(13, 1);
    Ponto nNorte1 = new Ponto(7, 14);
    Ponto nNorte2 = new Ponto(13, 14);

    // ========================================================
    // 2. CREATE ROUTES (Multi-segment paths between ports)
    // ========================================================
    List<Route> rotas = Arrays.asList(
        // Route 1: Southern coast (Lisboa → Faro)
        new Route(Arrays.asList(pLisboa, nSul1, nSul2, pFaro)),
        
        // Route 2: Northern coast (Vigo → Sagres)
        new Route(Arrays.asList(pVigo, nNorte1, nNorte2, pSagres)),
        
        // Route 3: Diagonal ascent (Lisboa → Center → Sagres)
        new Route(Arrays.asList(pLisboa, new Ponto(5, 4), pLeixoes, 
                                new Ponto(15, 10), pSagres))
    );

    // ========================================================
    // 3. MAP PORTS (For GUI dropdown menus)
    // ========================================================
    Map<String, Ponto> posicoesPortos = new HashMap<>();
    posicoesPortos.put("Porto de Lisboa", pLisboa);
    posicoesPortos.put("Porto de Faro", pFaro);
    posicoesPortos.put("Porto de Vigo", pVigo);
    posicoesPortos.put("Porto de Sagres", pSagres);
    posicoesPortos.put("Porto de Leixões", pLeixoes);

    // ========================================================
    // 4. DEFINE STATIC OBSTACLES
    // ========================================================
    
    // Island (polygon obstacle)
    Poligono ilhaNorte = new Poligono(new Ponto[]{
        new Ponto(8.5, 10), new Ponto(10, 12.5), 
        new Ponto(11.5, 11), new Ponto(11.5, 9.5), 
        new Ponto(10, 8.5), new Ponto(9, 9)
    });
    
    // Shallow waters (rectangle obstacle)
    Retangulo bancoDeAreia = new Retangulo(new Ponto[]{
        new Ponto(6, 2), new Ponto(14, 2), 
        new Ponto(14, 3), new Ponto(6, 3)
    });
    
    // Rock formation (complex polygon)
    Poligono rochasEste = new Poligono(new Ponto[]{
        new Ponto(16, 4.5), new Ponto(17.5, 6), 
        new Ponto(16, 6.5), new Ponto(14.5, 5)
    });
    
    // Coral reef (square obstacle)
    Quadrado recifeSul = new Quadrado(new Ponto[]{
        new Ponto(12, 4), new Ponto(13, 4), 
        new Ponto(13, 5), new Ponto(12, 5)
    });

    List<Poligono> obstaculosEstaticos = Arrays.asList(
        ilhaNorte, bancoDeAreia, rochasEste, recifeSul
    );
    List<Obstaculo> todosObstaculos = new ArrayList<>(obstaculosEstaticos);

    // ========================================================
    // 5. INITIALIZE SIMULATION ENGINE & CONTROL TOWER
    // ========================================================
    TorreDeControlo torre = new GestorMaritimo();

    // Create harbors
    Porto porto1 = new Porto("Porto de Lisboa", pLisboa, torre);
    Porto porto2 = new Porto("Porto de Faro", pFaro, torre);
    Porto porto3 = new Porto("Porto de Vigo", pVigo, torre);
    Porto porto4 = new Porto("Porto de Sagres", pSagres, torre);
    Porto porto5 = new Porto("Porto de Leixões", pLeixoes, torre);

    List<Porto> portos = Arrays.asList(porto1, porto2, porto3, porto4, porto5);

    // ========================================================
    // 6. REQUEST OCEAN CURRENT (User Input via Dialog)
    // ========================================================
    // Default current: (1.0, 1.0)
    Vetor corrente = DialogoCorrente.pedirCorrente(new Vetor(1.0, 1.0));
    if (corrente == null) System.exit(0);

    // ========================================================
    // 7. CREATE SIMULATOR
    // ========================================================
    Simulador simulador = new Simulador(
        corrente,      // Ocean current vector
        rotas,         // List of available routes
        portos,        // List of harbors
        todosObstaculos, // List of static obstacles
        torre          // Traffic control tower
    );

    // Create 3 mobile storm entities
    List<Tempestade> tempestadesParaGUI = new ArrayList<>();
    for (int i = 0; i < 3; i++) {
        tempestadesParaGUI.add(simulador.criarTempestade());
    }

    // ========================================================
    // 8. SCHEDULE TRAFFIC (Ships departing at different times)
    // ========================================================
    Runnable criarBarcos = () -> {
        // Immediate departures (converging to center)
        porto1.adicionarNavio(2.5, 0, porto4);    // Speed, delay (ms), destination
        porto3.adicionarNavio(2.2, 0, porto2);
        
        // Short-term departures (5-12 seconds)
        porto2.adicionarNavio(2.0, 5000, porto1);
        porto4.adicionarNavio(1.8, 8000, porto3);
        porto1.adicionarNavio(3.5, 10000, porto5); // Fast vessel
        
        // Medium-term departures (20-35 seconds)
        porto2.adicionarNavio(2.4, 20000, porto5);
        porto4.adicionarNavio(1.5, 25000, porto1); // Slow vessel
        
        // Long-term departures (45-65 seconds)
        porto3.adicionarNavio(2.6, 45000, porto2);
        porto2.adicionarNavio(1.8, 50000, porto3);
    };

    criarBarcos.run();

    // ========================================================
    // 9. START GUI AND SIMULATION
    // ========================================================
    SwingUtilities.invokeLater(() -> {
        simulador.iniciar();  // Start simulation engine
        JanelaPrincipal gui = new JanelaPrincipal(
            simulador,           // Simulation engine
            rotas,               // Routes to render
            obstaculosEstaticos, // Obstacles to render
            tempestadesParaGUI,  // Storms to render
            posicoesPortos,      // Port positions for GUI
            corrente,            // Ocean current (for display)
            criarBarcos          // Traffic scheduling callback
        );
        gui.iniciar();  // Launch window
    });
}
```

### Key Input Parameters Explained:

| Parameter | Type | Example | Description |
|-----------|------|---------|-------------|
| **Ponto** | Coordinates | `new Ponto(10, 7)` | Geometric point with X, Y coordinates |
| **Vetor** | Current | `new Vetor(1.0, 1.0)` | Ocean current direction and magnitude |
| **Route** | Path | `new Route(Arrays.asList(...))` | Multi-segment navigation path between ports |
| **Porto** | Harbor | `new Porto("name", point, tower)` | Named harbor at a geographic location |
| **Obstaculo** | Barrier | `new Poligono/Retangulo/...` | Static obstacle (island, reef, shallow water) |
| **Ship Speed** | Float | `2.5` | Vessel speed (units per second) |
| **Delay** | Long | `5000` | Departure delay in milliseconds |
| **Destination** | Porto | `porto4` | Target harbor for ship journey |

---

## 🧪 Running Tests

Unit tests are located under the `test/` directory. If using JUnit:

```bash
# Example running tests via javac/java with JUnit standalone console runner:
javac -d bin -cp "bin:lib/junit-platform-console-standalone.jar" src/**/*.java test/Engine/*.java
java -jar lib/junit-platform-console-standalone.jar --class-path bin --scan-class-path

```

---

## 📜 License

This project is developed for educational and research purposes in maritime simulation and object-oriented software engineering.
