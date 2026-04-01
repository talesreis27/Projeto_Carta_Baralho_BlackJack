# 🃏 Blackjack em Python

Um jogo de **Blackjack** implementado em Python utilizando Programação Orientada a Objetos (POO). O projeto conta com a classe `Carta`, a classe `Baralho` e a função principal `blackjack()` que gerencia toda a lógica do jogo no terminal.

---

## 📋 Sobre o Projeto

Este projeto foi desenvolvido com o objetivo de praticar os conceitos de POO em Python, simulando um jogo clássico de cassino — o Blackjack — diretamente no terminal. O jogador compete contra um dealer seguindo as regras tradicionais do jogo.

---

## 🗂️ Estrutura do Código

### `class Carta`
Representa uma carta individual do baralho.

- **Atributos de classe:**
  - `valores`: lista com os valores possíveis (`'2'` a `'10'`, `'J'`, `'Q'`, `'K'`, `'A'`)
  - `naipes`: lista com os naipes (`'Copas'`, `'Ouros'`, `'Paus'`, `'Espadas'`)
- **Métodos:**
  - `__init__(valor, naipe)` — inicializa a carta
  - `__lt__` / `__gt__` — permite comparação e ordenação entre cartas
  - `__str__` — retorna a representação textual (ex: `"A de Espadas"`)

### `class Baralho`
Representa um baralho completo com 52 cartas.

- **Métodos:**
  - `__init__()` — gera todas as 52 cartas (13 valores × 4 naipes)
  - `embaralhar()` — embaralha as cartas aleatoriamente
  - `retirar_carta()` — remove e retorna a primeira carta do baralho
  - `organizar()` — ordena as cartas do baralho

### `def blackjack()`
Função principal que controla o fluxo do jogo:

1. Cria e embaralha o baralho
2. Distribui 2 cartas iniciais para o jogador e para o dealer
3. Exibe as cartas do jogador e apenas a primeira carta do dealer
4. Calcula a pontuação inicial
5. Permite ao jogador escolher **HIT** (pedir carta) ou **STAND** (ficar)
6. O dealer joga automaticamente (compra cartas até atingir 17+ pontos)
7. Determina o vencedor com base nas pontuações finais

---

## 🎮 Regras do Jogo

| Carta | Pontuação |
|-------|-----------|
| 2 – 9 | Valor nominal |
| 10, J, Q, K | 10 pontos |
| A (Ás) | 11 pontos (ou 1, se necessário para não estourar) |

- **Objetivo:** chegar o mais próximo de **21 pontos** sem ultrapassar.
- **Blackjack:** mão inicial com 21 pontos — vitória imediata.
- **Estouro:** ultrapassar 21 pontos — derrota imediata.
- **Dealer:** sempre compra cartas enquanto tiver menos de 17 pontos.

---

## ▶️ Como Executar

### Pré-requisitos

- Python 3.x instalado

### Passos

```bash
# Clone o repositório
git clone https://github.com/talesreis27/Projeto_Carta_Baralho_BlackJack.git

# Acesse a pasta do projeto
cd Projeto_Carta_Baralho_BlackJack

# Execute o arquivo
python "Projeto Carta Baralho BlackJack.py.md"
```

> **Nota:** O código está salvo com extensão `.py.md`. Para executar diretamente pelo Python, renomeie o arquivo para `blackjack.py`.

---

## 💻 Exemplo de Execução

```
Bem-vindo ao jogo de Blackjack!
O baralho foi embaralhado. Vamos começar o jogo!
==================================================
Distribuindo as cartas iniciais...
Cartas distribuídas!
Cartas do dealer: 7 de Copas e uma carta oculta
Suas cartas: K de Espadas e 5 de Ouros
==================================================
Total de pontos do jogador: 15
Total de pontos do dealer: 7
Deseja 'HIT' para pedir mais cartas ou 'STAND' para ficar com as cartas que ja possui? HIT
Suas cartas: [K de Espadas, 5 de Ouros, 4 de Paus] - Total de pontos: 19
Deseja 'HIT' para pedir mais cartas ou 'STAND' para ficar com as cartas que ja possui? STAND
...
Parabéns! Você venceu!
```

---

## 📁 Arquivos do Repositório

```
Projeto_Carta_Baralho_BlackJack/
├── Projeto Carta Baralho BlackJack.py.md   # Código-fonte do jogo
├── LICENSE                                  # Licença MIT
└── README.md                                # Este arquivo
```

---

## 🛠️ Tecnologias Utilizadas

- **Python 3** — linguagem principal
- **Módulo `random`** (`shuffle`) — para embaralhar o baralho

---

## 📄 Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE) — sinta-se livre para usar, modificar e distribuir.

---

## 👤 Autor

**Tales Reis e Silva**  
GitHub: [@talesreis27](https://github.com/talesreis27)
