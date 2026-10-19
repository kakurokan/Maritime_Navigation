# Trabalho 1 — POO

[![CI](https://github.com/kakurokan/Maritime_Navigation/actions/workflows/ci.yml/badge.svg)](https://github.com/kakurokan/Maritime_Navigation/actions/workflows/ci.yml)

Simulador de navegação marítima: navios calculam rotas entre portos (Dijkstra sobre um grafo),
evitam obstáculos e tempestades, e são coordenados por uma torre de controlo. Inclui uma interface
gráfica em Swing.

## Build and test

Requirements:

- **JDK 25** (the entry point `Cliente.java` uses a top-level `void main()`, final since Java 25)
- **Maven 3.9+**

Run the test suite:

```sh
mvn test
```

Compile and launch the simulator:

```sh
mvn compile
java -cp target/classes Cliente
```

Project layout:

```
src/main/java/Cliente.java   entry point
src/main/java/Engine/        simulation model (geometry, routing, ships, ports)
src/main/java/GUI/           Swing interface
src/test/java/Engine/        JUnit 5 tests
```

CI runs `mvn -B test` on every push and pull request (`.github/workflows/ci.yml`).
