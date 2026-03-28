# Prática 3: Sincronização de Tarefas com Mutex (FreeRTOS) 🛡️
### Este repositório apresenta a resolução da Prática 3 da disciplina de Sistemas Operacionais Embarcados na UFPR. O foco é a eliminação de condições de corrida através de mecanismos de sincronização.
## 🎯 Objetivos Didáticos
1. **Exclusão Mútua (Mutex):** Implementação de `xSemaphoreCreateMutex` para gerenciar o acesso ao LCD 16x2.
2. **Sincronização de Recursos Compartilhados:** Garantir que as tarefas `TaskSlider` (Core 0) e `TaskTemp` (Core 1) não acessem o barramento do display simultaneamente.
3. **Gerenciamento de Timeouts:** Uso de `xSemaphoreTake` com tempo de espera definido para evitar o bloqueio indefinido de tarefas.
## 🛠️ Solução Técnica
Diferente da Prática 2, onde os dados eram corrompidos, aqui o acesso ao recurso físico é protegido por um "token" (o Mutex):
* Antes de escrever no LCD, a tarefa deve "tomar" o semáforo.
* Caso o semáforo esteja ocupado por outra tarefa, a tarefa atual aguarda.
* Após a escrita, a tarefa "devolve" o semáforo, liberando o periférico para o próximo processo.
## 🚀 Como Executar
1. O código principal está localizado no arquivo sketch.ino.
2. As conexões de hardware estão descritas no arquivo diagram.json.
3. As bibliotecas estão especificadas no arquivo libraries.txt 
4. **Simulação Online:** Você pode testar o comportamento do sistema diretamente no navegador:
    * ▶️ [Link para a Simulação no Wokwi](https://wokwi.com/projects/436019129502895105) 


---
### Prof. Thiago José da Luz, PhD 