# Maritime Navigation Simulator

[![Java](https://img.shields.io/badge/Java-8%2B-ED8B00?logo=java&logoColor=white)](https://www.oracle.com/java/)
[![Swing](https://img.shields.io/badge/UI-Swing-007396?logo=java&logoColor=white)](https://docs.oracle.com/javase/tutorial/uiswing/)
[![Status](https://img.shields.io/badge/Status-Academic%20Project-28a745)](https://github.com/kakurokan/Maritime_Navigation)
[![Platform](https://img.shields.io/badge/Platform-Desktop%20App-000000)](https://github.com/kakurokan/Maritime_Navigation)

A Java-based desktop simulator for modeling maritime traffic, vessel navigation, route planning, and environmental dynamics in a controlled virtual environment.

This project was developed as an academic exercise in object-oriented software design, graph-based pathfinding, geometric modeling, and GUI programming using Swing. It emphasizes the separation of concerns between simulation logic and presentation, while demonstrating core design patterns commonly used in software engineering.

## Overview

The application simulates ships moving through a maritime environment under a set of constraints and operational rules. It integrates several components:

- vessel movement and state management;
- dynamic route computation and navigation strategies;
- obstacle and geometry handling;
- maritime traffic coordination;
- environmental conditions such as currents and storms;
- real-time visualization in a desktop interface.

The system is designed to support experimentation with navigation logic, path optimization, and simulation behavior in a modular architecture.

## Key Features

- Maritime vessel simulation with state transitions
- Autonomous navigation and route-following behavior
- Graph-based route optimization using pathfinding strategies
- Geometric modeling for obstacles, ports, and spatial constraints
- Environmental simulation including currents and storm effects
- Traffic management and harbor coordination logic
- Interactive desktop interface built with Java Swing
- Modular structure suitable for academic extension and testing

## Architecture and Design Patterns

The project follows a layered architecture that separates the simulation engine from the graphical interface:

- `src/Engine/`: core simulation logic, geometry, graph structures, navigation rules, and entities
- `src/GUI/`: Swing components for user interaction and visual rendering
- `src/Cliente.java`: application entry point
- `test/Engine/`: validation of simulation-related behavior

The implementation uses several software design patterns, including:

- Strategy Pattern: `EstrategiaRota` and `EstrategiaDijkstra`
- State Pattern: `EstadoMovel` and its concrete states
- Memento/Snapshot Pattern: `SnapshotSimulacao`
- Separation of responsibilities between engine and interface layers

## Project Structure

```text
Maritime_Navigation/
├── README.md
├── Projeto1.iml
├── src/
│   ├── Cliente.java
│   ├── Engine/
│   │   ├── AutoPilot.java
│   │   ├── Circulo.java
│   │   ├── EstadoMovel.java
│   │   ├── EstrategiaDijkstra.java
│   │   ├── EstrategiaRota.java
│   │   ├── GestorMaritimo.java
│   │   ├── Grafo.java
│   │   ├── Movel.java
│   │   ├── Navio.java
│   │   ├── Navegante.java
│   │   ├── Obstaculo.java
│   │   ├── Ponto.java
│   │   ├── Porto.java
│   │   ├── Route.java
│   │   ├── SegmentoReta.java
│   │   ├── Simulador.java
│   │   ├── SnapshotSimulacao.java
│   │   ├── Tempestade.java
│   │   ├── TorreDeControlo.java
│   │   ├── Triangulo.java
│   │   └── Vetor.java
│   └── GUI/
│       ├── AcaoAlternarDirecao.java
│       ├── AcaoReiniciarSimulacao.java
│       ├── DialogoCorrente.java
│       ├── JanelaPrincipal.java
│       └── PainelMapa.java
└── test/
    └── Engine/
```

## Requirements

- Java Development Kit (JDK) 8 or later
- A Java-compatible IDE is recommended, such as IntelliJ IDEA, Eclipse, or VS Code with Java support
- A desktop environment capable of running Swing-based applications

## Installation and Execution

### 1. Clone the repository

```bash
git clone https://github.com/kakurokan/Maritime_Navigation.git
cd Maritime_Navigation
```

### 2. Compile the project

```bash
mkdir -p bin
find src -name "*.java" > sources.txt
javac -d bin @sources.txt
rm sources.txt
```

### 3. Run the application

```bash
java -cp bin Cliente
```

## Runtime Behavior

When the application starts, the user may be prompted to enter the ocean current parameters used by the simulator. These values influence vessel trajectories and the overall simulation dynamics.

Representative examples include:

- no current: `0.0, 0.0`
- weak current: `0.5, 0.5`
- moderate current: `1.0, 1.0`
- strong current: `2.5, 2.5`

The interface allows interaction with the simulation and observation of movement over a map-based visualization.

## Testing

The repository includes test classes under the `test/Engine` directory for validating simulation-related logic, geometry, vectors, and route behavior.

Depending on the toolchain used, tests may be executed through the IDE or by configuring a JUnit-based workflow in the project environment.

## Academic Relevance

This project is relevant to several topics in computer science and software engineering, including:

- object-oriented programming;
- graph theory and shortest-path algorithms;
- simulation design;
- geometric modeling and collision logic;
- software architecture and modularization;
- GUI development and event-driven interfaces.

## Notes

This project was developed for educational and research purposes, with emphasis on simulation logic and software design practice.

## License

No formal license file is currently present in the repository. The code should be used with caution and in accordance with the repository owner’s intended usage policy before reuse in external academic or commercial contexts.

## Contributing

Contributions are welcome in the form of improvements to the simulation engine, graphical interface, documentation, or test coverage. If you intend to contribute, please open an issue or submit a pull request with a clear description of the proposed changes.
