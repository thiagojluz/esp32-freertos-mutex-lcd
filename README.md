# Prática 3: Sincronização de Tarefas com Mutex (FreeRTOS) 🛡️

Este repositório apresenta o desenvolvimento da **Prática 3** da disciplina de **Sistemas Operacionais Embarcados**, ministrada no **Departamento de Engenharia Elétrica da Universidade Federal do Paraná (UFPR)**.  
O projeto tem como foco a **eliminação de condições de corrida** em sistemas embarcados **multitarefa e multicore**, utilizando **mecanismos de exclusão mútua (Mutex)** providos pelo **FreeRTOS**.

Esta prática dá continuidade direta à **Prática 2**, resolvendo o problema de acesso concorrente ao display LCD por meio de sincronização adequada.

---

## 🎯 Objetivos Didáticos

1. **Exclusão Mútua (Mutex):**  
   Implementação de `xSemaphoreCreateMutex` para controlar o acesso concorrente ao display LCD 16x2.

2. **Sincronização de Recursos Compartilhados:**  
   Garantir que as tarefas `TaskSlider` (Core 0) e `TaskTemp` (Core 1) não realizem escrita simultânea no barramento paralelo do display.

3. **Gerenciamento de Timeouts:**  
   Utilização de `xSemaphoreTake` com tempo máximo de espera, evitando bloqueio indefinido e promovendo maior robustez do sistema.

---

## 🧠 Competências Demonstradas

- Programação de sistemas embarcados com **FreeRTOS**
- Implementação de **Mutexes** para proteção de recursos compartilhados
- Sincronização segura de tarefas em **arquitetura dual-core (ESP32)**
- Compreensão prática de **condições de corrida e exclusão mútua**
- Gerenciamento de **timeouts e bloqueios controlados**
- Análise de comportamento determinístico em sistemas de tempo real
- Projeto incremental de sistemas embarcados com foco em confiabilidade

---

## 🛠️ Solução Técnica

Diferentemente da **Prática 2**, onde ocorria corrupção de dados no display LCD, nesta implementação o acesso ao recurso físico é protegido por um **Mutex**, funcionando como um *token de acesso exclusivo*.

A lógica de funcionamento é a seguinte:

- Antes de acessar o LCD, a tarefa solicita o Mutex utilizando `xSemaphoreTake`.
- Caso o Mutex esteja indisponível, a tarefa aguarda até o tempo máximo configurado.
- Após finalizar a escrita no display, a tarefa libera o Mutex com `xSemaphoreGive`.
- Somente uma tarefa por vez pode acessar o barramento do display, garantindo comunicação íntegra.

Essa abordagem elimina completamente o problema de concorrência observado anteriormente.

---

## 🛠️ Hardware Utilizado (Simulado no Wokwi)

- **Microcontrolador:** ESP32  
- **Sensores:**  
  - DHT22 (Temperatura)  
  - Potenciômetro (Slider)  
- **Display:** LCD 16x2 em modo paralelo (sem I²C)

---

## 💡 Relevância Técnica

O uso correto de **Mutexes** é fundamental em sistemas embarcados reais que operam em **ambiente multitarefa**, especialmente em arquiteturas **multicore**.  
Este projeto reproduz um cenário típico encontrado em aplicações **industriais, automotivas e de IoT**, onde múltiplas tarefas competem por recursos físicos limitados.  

A prática evidencia como mecanismos de sincronização são essenciais para garantir:
- integridade dos dados;
- comportamento determinístico;
- confiabilidade do sistema;
- escalabilidade da solução.

---

## 🚀 Como Executar

1. O código principal está localizado no arquivo `sketch.ino`.
2. As conexões de hardware estão descritas no arquivo `diagram.json`.
3. As bibliotecas utilizadas estão especificadas no arquivo `libraries.txt`.
4. **Simulação Online:**  
   O comportamento do sistema pode ser testado diretamente no navegador por meio do link abaixo:  
   ▶️ https://wokwi.com/projects/436019129502895105

---

## 🧪 Validação e Testes

- Execução simultânea das tarefas em núcleos distintos.
- Verificação da escrita correta e estável no display LCD.
- Avaliação do comportamento do sistema sob múltiplos acessos concorrentes.
- Confirmação da ausência de corrupção de caracteres após a implementação do Mutex.
- Observação do impacto do timeout no escalonamento das tarefas.

---

## ✅ Resultado da Sincronização

Após a implementação do **Mutex**, o sistema apresenta:

- Atualização consistente do display LCD;
- Eliminação completa da condição de corrida;
- Acesso ordenado e seguro ao periférico compartilhado;
- Comportamento previsível mesmo em ambiente multitarefa.

---

## 📚 Evolução do Projeto

Esta prática completa o ciclo conceitual iniciado nas práticas anteriores:

- **Prática 1:** Operação reativa com interrupções em ambiente bare-metal  
- **Prática 2:** Identificação de condições de corrida em multitarefa multicore  
- **Prática 3:** Correção da concorrência utilizando mecanismos de sincronização  

Como próxima evolução, o portfólio pode explorar:
- Uso de **Filas (Queues)** para comunicação entre tarefas
- Uso de IoT

---

**Prof. Thiago José da Luz, PhD**  
Departamento de Engenharia Elétrica – UFPR
