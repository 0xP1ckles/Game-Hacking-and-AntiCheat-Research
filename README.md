
# Game Hacking & Anti-Cheat Research

 English |  Português

A personal research and learning project focused on Game Hacking,
Reverse Engineering, Memory Analysis, and Anti-Cheat Security.

---

#  English

## About the Project

This repository documents my learning journey in **Game Hacking,
Reverse Engineering, Memory Analysis, and Anti-Cheat Research**.

The main objective is to understand how video games manage memory,
how vulnerabilities can be exploited in controlled environments,
and how security mechanisms can detect and prevent unauthorized
manipulation.

This project combines offensive security research with defensive
techniques, focusing on practical experiments and technical
documentation.

## Learning Objectives

- Understand C/C++ fundamentals and memory management.
- Explore pointers, memory addresses, and data structures.
- Study how games store and manipulate information in memory.
- Learn reverse engineering and debugging techniques.
- Develop proof-of-concept experiments in controlled environments.
- Understand game security vulnerabilities.
- Research anti-cheat detection and prevention mechanisms.
- Develop practical offensive and defensive security skills.

## Lab 01 — Memory Fundamentals

**Status:** ✅ Completed

### Topics Covered

- C++ variables and data types
- Memory addresses
- Pointers and dereferencing
- Reading and modifying memory values
- Memory addresses across different executions
- Introduction to memory manipulation

### Experiment

Developed a simple C++ application simulating a player's health.

The application initializes the player's health at `100` and
displays its memory address.

A pointer is then used to access the variable and modify its
value from `100` to `999`.

### Key Findings

- Variables have values and associated memory locations.
- Pointers store memory addresses.
- The `&` operator retrieves a variable's address.
- The `*` operator dereferences a pointer.
- Dereferencing allows reading and modifying values.
- Changing a value through a pointer does not change its address.
- Memory addresses may vary between program executions.

### Development Environment

- Windows 11 Pro x64 (Virtual Machine)
- Visual Studio Community
- C++
- Debug x64

---

#  Português

## Sobre o Projeto

Este repositório documenta o meu percurso de aprendizagem em
**Game Hacking, Engenharia Inversa, Análise de Memória e
Investigação de Sistemas Anti-Cheat**.

O principal objetivo é compreender como os videojogos gerem a
memória, como determinadas vulnerabilidades podem ser exploradas
em ambientes controlados e como os mecanismos de segurança
conseguem detetar e prevenir manipulações não autorizadas.

Este projeto combina investigação em segurança ofensiva com
técnicas defensivas, privilegiando experiências práticas e
documentação técnica.

## Objetivos de Aprendizagem

- Compreender os fundamentos de C/C++ e gestão de memória.
- Explorar ponteiros, endereços de memória e estruturas de dados.
- Estudar como os jogos armazenam e manipulam informação na memória.
- Aprender técnicas de engenharia inversa e debugging.
- Desenvolver provas de conceito em ambientes controlados.
- Compreender vulnerabilidades de segurança em videojogos.
- Investigar mecanismos de deteção e prevenção anti-cheat.
- Desenvolver competências práticas de segurança ofensiva e defensiva.

## Laboratório 01 — Fundamentos de Memória

**Estado:** ✅ Concluído

### Conceitos Abordados

- Variáveis e tipos de dados em C++
- Endereços de memória
- Ponteiros e desreferenciação
- Leitura e modificação de valores na memória
- Endereços de memória entre diferentes execuções
- Introdução à manipulação de memória

### Experiência Realizada

Desenvolvi uma aplicação simples em C++ que simula o valor
de vida de um jogador.

A aplicação inicializa a vida do jogador com o valor `100`
e apresenta o respetivo endereço de memória.

Posteriormente, utilizei um ponteiro para aceder à variável
e modificar o seu valor de `100` para `999`.

### Principais Conclusões

- As variáveis possuem valores e localizações na memória.
- Os ponteiros armazenam endereços de memória.
- O operador `&` permite obter o endereço de uma variável.
- O operador `*` permite desreferenciar um ponteiro.
- A desreferenciação permite ler e modificar valores.
- Alterar um valor através de um ponteiro não modifica o endereço.
- Os endereços de memória podem variar entre execuções.

### Ambiente de Desenvolvimento

- Windows 11 Pro x64 (Máquina Virtual)
- Visual Studio Community
- C++
- Debug x64

---

# Research Roadmap / Plano de Investigação

| Lab | Topic / Tema | Status / Estado |
|-----|--------------|-----------------|
| 01 | Memory Fundamentals / Fundamentos de Memória | ✅ Completed / Concluído |
| 02 | Memory Layout & Offsets | ⏳ Planned / Planeado |
| 03 | Reverse Engineering & Assembly | ⏳ Planned / Planeado |
| 04 | Game Memory Analysis | ⏳ Planned / Planeado |
| 05 | Anti-Cheat Detection & Research | ⏳ Planned / Planeado |
| 06 | Game Security — Attack & Defense | ⏳ Planned / Planeado |

---

# Research Methodology / Metodologia

###  English

Each laboratory follows a structured learning methodology:

1. Study the theoretical concepts.
2. Develop a practical experiment.
3. Observe and analyze the results.
4. Document the techniques and findings.
5. Identify potential security implications.
6. Explore defensive approaches when applicable.

###  Português

Cada laboratório segue uma metodologia de aprendizagem estruturada:

1. Estudar os conceitos teóricos.
2. Desenvolver uma experiência prática.
3. Observar e analisar os resultados.
4. Documentar as técnicas e conclusões.
5. Identificar possíveis implicações de segurança.
6. Explorar abordagens defensivas quando aplicável.

---

# Disclaimer / Aviso

###  English

All experiments are conducted in controlled environments using
self-developed applications or explicitly authorized targets.

This repository is intended exclusively for educational purposes,
security research, and defensive development.

###  Português

Todas as experiências são realizadas em ambientes controlados,
utilizando aplicações desenvolvidas por mim ou sistemas para os
quais existe autorização explícita.

Este repositório destina-se exclusivamente à aprendizagem,
investigação em cibersegurança e desenvolvimento de mecanismos
defensivos.
