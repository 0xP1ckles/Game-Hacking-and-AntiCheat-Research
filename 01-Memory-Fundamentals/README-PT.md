# DIA 1 - Cheating LAB

> **Estado:** Concluído  
> **Ambiente:** C++ · Visual Studio Community · Windows 11 Pro x64 (VM) · Debug x64

## Objetivos do dia

- Entender os fundamentos de C/C++ aplicados a jogos.
- Compreender variáveis, ponteiros e endereços de memória.
- Observar a leitura e a alteração de valores com o debugger.
- Explorar a organização de uma `struct` e os respetivos offsets.

---

## 1. Primeiro teste - Ler uma variável através de um ponteiro

### Código utilizado

```cpp
#include <iostream>

int main() {
    int health = 100;

    // Guardar o endereco da variavel
    int* healthPtr = &health;

    std::cout << "=== GAME HACKING LAB 01 ===\n";

    std::cout << "Health: " << health << "\n";
    std::cout << "Address: " << &health << "\n";
    std::cout << "Pointer: " << healthPtr << "\n";
    std::cout << "Value via pointer: " << *healthPtr << "\n";

    return 0;
}
```

![Leitura inicial: valor da variável, endereço e ponteiro](images/image.png)

**Observação:** O endereço apresentado por `&health` coincide com o endereço guardado em `healthPtr`. O acesso por `*healthPtr` devolve o valor `100`.

## 2. Segundo teste - Alterar o valor através de um ponteiro

### Código utilizado

```cpp
#include <iostream>

int main() {
    int health = 100;

    // Guardar o endereco da variavel
    int* healthPtr = &health;

    std::cout << "=== GAME HACKING LAB 01 ===\n";

    std::cout << "Health: " << health << "\n";
    std::cout << "Address: " << &health << "\n";
    std::cout << "Pointer: " << healthPtr << "\n";
    std::cout << "Value via pointer: " << *healthPtr << "\n";

    // Alterar a memoria atraves do ponteiro
    *healthPtr = 999;

    std::cout << "\n=== AFTER MODIFICATION ===\n";
    std::cout << "New Health: " << health << "\n";

    return 0;
}
```

![Resultado da alteração: health passa de 100 para 999](images/image-1.png)

**Observação:** Ao escrever `*healthPtr = 999`, modificámos a variável original, e não uma cópia do valor.

## 3. Análise com o debugger do Visual Studio

Colocámos um breakpoint antes da instrução `*healthPtr = 999;` para observar o conteúdo da memória antes e depois da alteração.

Para iniciar a depuração, utilizámos **F5**. Para avançar instrução a instrução, utilizámos **F10** (*Step Over*). A janela de memória permitiu inspecionar os bytes no endereço observado.

### 3.1. Breakpoint antes da alteração

![Código no Visual Studio com breakpoint na instrução de alteração](images/image-2.png)

### 3.2. Memória antes da alteração

Antes de executar a instrução, encontrámos o valor de `health` correspondente a **100** em decimal, ou **`0x64`** em hexadecimal.

![Visualização da memória antes da alteração](images/image-3.png)

### 3.3. Memória depois da alteração

Ao avançar com **F10** e executar a instrução, observámos o valor passar para **999** em decimal, equivalente a **`0x3E7`** em hexadecimal.

![Visualização da memória depois da alteração](images/image-4.png)

**Interpretação:** O operador `*` permite aceder ao conteúdo do endereço guardado pelo ponteiro. Quando escrevemos `*healthPtr = 999`, modificamos a variável original, sem alterar o endereço para o qual o ponteiro aponta.

---

## 4. Terceiro teste - Estrutura `Player`

### Código utilizado

```cpp
#include <iostream>
#include <cstddef>

struct Player {
    int health = 100;
    int ammo = 30;
    float speed = 5.0f;
};

int main() {
    Player player;

    std::cout << "=== GAME HACKING LAB 01 ===\n";

    // Valores iniciais do jogador
    std::cout << "\n=== PLAYER STATS ===\n";
    std::cout << "Health: " << player.health << "\n";
    std::cout << "Ammo: " << player.ammo << "\n";
    std::cout << "Speed: " << player.speed << "\n";

    // Enderecos de memoria
    std::cout << "\n=== MEMORY ADDRESSES ===\n";
    std::cout << "Health: " << &player.health << "\n";
    std::cout << "Ammo: " << &player.ammo << "\n";
    std::cout << "Speed: " << &player.speed << "\n";

    // Offsets dos atributos na estrutura
    std::cout << "\n=== MEMORY OFFSETS ===\n";
    std::cout << "Health offset: "
        << offsetof(Player, health) << "\n";

    std::cout << "Ammo offset: "
        << offsetof(Player, ammo) << "\n";

    std::cout << "Speed offset: "
        << offsetof(Player, speed) << "\n";

    // Tamanho total da estrutura
    std::cout << "\n=== STRUCT SIZE ===\n";
    std::cout << "Player size: "
        << sizeof(Player) << " bytes\n";

    // Colocar breakpoint nesta linha (F9)
    player.health = 999;

    // Verificar alteracao
    std::cout << "\n=== AFTER MODIFICATION ===\n";
    std::cout << "New Health: " << player.health << "\n";
    std::cout << "Ammo: " << player.ammo << "\n";
    std::cout << "Speed: " << player.speed << "\n";

    return 0;
}
```

> **Nota:** O ficheiro [`LAB.cpp`](LAB.cpp) contém esta versão final do terceiro teste. Os códigos dos dois primeiros testes encontram-se documentados nas secções anteriores.

### 4.1. Estrutura de um `Player`

Uma `struct` em C++ permite agrupar várias variáveis relacionadas dentro de um único tipo de dados.

Neste laboratório, criámos uma estrutura `Player` com três atributos:

- `health` — vida do jogador (`int`).
- `ammo` — munição do jogador (`int`).
- `speed` — velocidade do jogador (`float`).

Cada atributo ocupa espaço em memória. No nosso ambiente Windows x64, `int` e `float` ocupam 4 bytes cada.

### 4.2. Organização da memória e offsets

Um **offset** representa a distância, em bytes, entre um endereço de referência e outro endereço. Numa estrutura, utilizamos o endereço inicial da estrutura como referência.

No exemplo observado, os atributos encontram-se em posições separadas por 4 bytes:

| Atributo | Tipo | Tamanho | Offset |
|---|---|---|---|
| `health` | `int` | 4 bytes | `0x00` |
| `ammo` | `int` | 4 bytes | `0x04` |
| `speed` | `float` | 4 bytes | `0x08` |

Assim, considerando o endereço inicial da estrutura como `0x1000`, teríamos:

- `health` → `0x1000`
- `ammo` → `0x1004`
- `speed` → `0x1008`

Nesta compilação, `sizeof(Player)` devolveu **12 bytes**. Esta disposição corresponde à estrutura utilizada neste laboratório, mas outras estruturas podem conter espaços de preenchimento (*padding*) devido a requisitos de alinhamento de memória.

### 4.3. Observação no debugger

Com o Visual Studio, observámos os endereços dos três atributos e inspecionámos os respetivos valores na janela de memória.

Neste **terceiro teste**, a instrução `player.health = 999;` modifica o atributo **diretamente**, sem recorrer a um ponteiro explícito. Isto é diferente do **segundo teste**, no qual utilizámos `*healthPtr = 999;` para modificar a variável através de um ponteiro.

A alteração de `player.health` de `100` para `999` modificou o valor da vida do jogador, enquanto `ammo` permaneceu em `30` e `speed` em `5.0`. Os offsets permaneceram iguais.

![Código C++ e execução do laboratório de memória](images/image-10.png)

![Resultados do laboratório com a estrutura Player](images/image-5.png)

![Estrutura Player: valores iniciais, endereços de memória e offsets](images/image-11.png)

![Alteração direta de Health de 100 para 999 e análise no debugger](images/image-8.png)

---

## 5. Conceitos teóricos

### 5.1. Variáveis e memória

Uma variável é um espaço de armazenamento associado a um tipo de dados e a um valor.

```cpp
int health = 100;
```

- `int` — tipo de dados (4 bytes no ambiente utilizado).
- `health` — nome da variável.
- `100` — valor inicial.

Durante a execução, o valor pode estar armazenado na memória física, sendo acedido através do espaço de endereçamento virtual do processo.

### 5.2. Endereços de memória

Cada byte de memória endereçável tem um endereço. O operador `&` permite obter o endereço de uma variável.

```cpp
std::cout << &health;
```

O endereço é normalmente apresentado em hexadecimal, com os caracteres `0–9` e `A–F`.

Os endereços podem variar entre execuções devido à organização da memória do processo e a mecanismos de segurança como o **ASLR** (*Address Space Layout Randomization*).

### 5.3. Ponteiros (*Pointers*)

Um ponteiro é uma variável que armazena um endereço de memória.

```cpp
int* healthPtr = &health;
```

- `int*` — declara um ponteiro para um inteiro.
- `healthPtr` — nome do ponteiro.
- `&health` — obtém o endereço da variável `health`.

O ponteiro não contém uma cópia do valor de `health`; contém o endereço onde esse valor está armazenado.

### 5.4. Desreferenciação (*Dereferencing*)

O operador `*`, aplicado a um ponteiro numa expressão, permite aceder ao valor armazenado no endereço apontado.

```cpp
std::cout << *healthPtr;
```

Resultado: `100`.

Também podemos escrever nesse endereço:

```cpp
*healthPtr = 999;
```

Neste caso, o valor de `health` passa de `100` para `999`.

**Importante:** Alterar o conteúdo de uma variável através de um ponteiro não significa alterar o endereço da variável.

### 5.5. Resumo dos operadores

| Expressão | Significado |
|---|---|
| `health` | Valor da variável |
| `&health` | Endereço da variável |
| `healthPtr` | Endereço guardado no ponteiro |
| `*healthPtr` | Valor no endereço apontado |
| `*healthPtr = 999` | Escrita no endereço apontado |

---

## 6. Relação com Game Hacking

Os jogos utilizam memória para armazenar dados como vida, munição, coordenadas e estados dos objetos.

Compreender ponteiros, estruturas e endereços é essencial para estudar como esses dados são organizados e manipulados.

Neste laboratório, modificámos a memória do nosso próprio programa. Futuramente, estudaremos como os debuggers e as ferramentas de análise de memória observam os processos em ambientes controlados e autorizados.

## 7. Resultados obtidos

- Compilámos um programa C++ em Windows x64.
- Obtivemos o endereço de uma variável.
- Criámos um ponteiro para essa variável.
- Lemos o valor através do ponteiro.
- Alterámos o valor de `100` para `999` através de um ponteiro no segundo teste.
- Criámos uma estrutura `Player` com vida, munição e velocidade.
- Identificámos os offsets `0`, `4` e `8`, bem como o tamanho total de `12` bytes nesta compilação.
- Alterámos diretamente `player.health` de `100` para `999` no terceiro teste.
- Observámos os valores antes e depois das alterações no debugger.
- Observámos endereços absolutos diferentes entre execuções, mantendo os offsets da estrutura.

**Aprendizagem principal:** Um ponteiro permite aceder indiretamente a uma variável através do seu endereço de memória. Os offsets permitem localizar membros de uma estrutura relativamente ao seu endereço inicial. Estes conceitos são fundamentais para compreender a análise de memória e a engenharia inversa.
