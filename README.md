# Maritime Navigation

Simulador marítimo desenvolvido em Java para modelar o movimento de embarcações, a navegação em rotas, a interação com obstáculos e a visualização em interface gráfica.

O projeto foi pensado como uma aplicação acadêmica para explorar conceitos de programação orientada a objetos, algoritmos de caminho, desenho geométrico e interfaces Swing.

## Visão geral

Este simulador permite:

- controlar e visualizar embarcações em movimento;
- definir rotas e caminhos com base em grafos e algoritmos de busca;
- simular condições ambientais como correntes marítimas e tempestades;
- modelar obstáculos geométricos e portos;
- acompanhar o estado de cada veículo durante a simulação;
- interagir com uma interface gráfica em Java Swing.

## Funcionalidades principais

- Navegação e autopilot de navios
- Planejamento de rotas com grafos e estratégia de caminho
- Geometria e colisão com obstáculos
- Simulação de corrente marítima e eventos ambientais
- Gestão de portos e tráfego marítimo
- Interface gráfica para visualização do mapa
- Testes unitários para a lógica do motor de simulação

## Estrutura do projeto

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

## Tecnologias

- Java
- Swing para interface gráfica
- Padrões de projeto como:
  - Strategy
  - State
  - Memento/Snapshot

## Requisitos

- JDK 8 ou superior
- IDE opcional: IntelliJ IDEA, Eclipse ou VS Code com suporte Java

## Como executar

1. Clone o repositório:

```bash
git clone https://github.com/kakurokan/Maritime_Navigation.git
cd Maritime_Navigation
```

2. Compile os arquivos Java:

```bash
mkdir -p bin
find src -name "*.java" > sources.txt
javac -d bin @sources.txt
rm sources.txt
```

3. Execute a aplicação:

```bash
java -cp bin Cliente
```

## Uso da simulação

Ao iniciar a aplicação, a interface solicitará valores para a corrente marítima. Esses valores influenciam o deslocamento dos navios e o comportamento da simulação.

Exemplos de entrada:

- sem corrente: `0.0, 0.0`
- corrente fraca: `0.5, 0.5`
- corrente moderada: `1.0, 1.0`
- corrente forte: `2.5, 2.5`

## Testes

Os testes do projeto ficam na pasta `test/Engine` e cobrem parte da lógica do motor de simulação, geometria, vetores e rota.

Para executar os testes, normalmente é necessário usar a IDE ou configurar o JUnit no projeto conforme a ferramenta escolhida.

## Padrões de projeto utilizados

- Strategy: troca de estratégia de rota por meio de `EstrategiaRota` e `EstrategiaDijkstra`
- State: gerenciamento dos estados de movimentação dos objetos (`MovelNaOrigem`, `MovelNavegando`, `MovelAguardando`, `MovelNoDestino`)
- Memento/Snapshot: captura do estado da simulação com `SnapshotSimulacao`
- Separação de responsabilidades: lógica de simulação em `Engine` e interface em `GUI`

## Observações

Este projeto foi desenvolvido com fins educacionais e de estudo em simulação marítima, programação orientada a objetos e arquitetura de software.

## Licença

O projeto não possui uma licença formal definida no repositório. Consulte o autor ou o contexto do uso antes de reutilizar o código em outros projetos.
