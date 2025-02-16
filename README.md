# ponderada_S1_afonsin

## Avaliação do Barema de Qualidade

### 1. Seleção de Serviços de Nuvem (Peso: 30%)
- **Escolha de serviços:** A arquitetura apresentada utiliza uma combinação de **RabbitMQ**, **Docker containers** e **bancos de dados organizados por camadas (Data Warehouse e DB Gold)**.
- **Justificativa:**
  - **RabbitMQ:** Escolhido como broker de mensagens para gerenciar filas de tarefas, garantindo comunicação assíncrona entre os componentes.
  - **Containers Docker:** Cada componente é isolado em um container para garantir portabilidade, escalabilidade e facilidade de manutenção.
  - **Data Warehouse:** Utilizado para armazenamento intermediário de dados após o processamento inicial.
  - **DB Gold:** Banco final para dados refinados e prontos para análise, garantindo consistência e otimização de consultas.
  - **Mecanismo de Cache:** Utilizado para reduzir a latência das consultas, armazenando resultados frequentemente acessados.
  - **Coleta de Dados ao Vivo:** Garante atualizações em tempo real para o DB Gold.

---

### 2. Elaboração do Desenho no Draw.io (Peso: 40%)
- **Representação visual clara e lógica:** O fluxo de dados foi organizado de forma sequencial, evidenciando o caminho das mensagens desde a fila RabbitMQ até a camada de apresentação.
- **Uso eficiente do espaço:** Componentes principais são facilmente identificáveis e conectados por setas que indicam o fluxo de informações.
- **Divisão lógica em camadas:**
  - **Fila de mensagens (RabbitMQ):** Primeiro componente que gerencia as tarefas a serem processadas.
  - **Containers Docker:** Cada componente está claramente envolvido por um contêiner, reforçando a arquitetura baseada em microserviços.
  - **Data Warehouse:** Camada intermediária para armazenamento e processamento de dados.
  - **DB Gold:** Camada final para dados refinados, com dois jobs automatizados para verificação e reconstrução de dados.
  - **Camada de apresentação:** Inclui coleta de dados ao vivo, mecanismo de cache e o componente de frontend.

---

### 3. Legenda Detalhada (Peso: 20%)
- **Legenda Inclusa:** Cada componente foi identificado no diagrama, detalhando sua função e papel no fluxo.
- **Descrição de componentes principais:**
  - **RabbitMQ:** Gerencia as mensagens entre componentes.
  - **Primeiro Componente:** Lê, trata e insere dados no Data Warehouse.
  - **Segundo Componente:** Cria views a partir dos dados no Data Warehouse e envia para o DB Gold.
  - **DB Gold:** Armazena os dados refinados, prontos para uso.
  - **Jobs Automatizados:** Reanálise e verificação periódica para garantir a integridade dos dados no DB Gold.
  - **Mecanismo de Cache Diário:** Melhora a eficiência do sistema, reduzindo a carga no banco.
  - **Componente de Frontend:** Interface de visualização dos dados processados.

---

### 4. Justificativa no Draw.io (Peso: 10%)
- **Notas explicativas:** Justificativas foram adicionadas para explicar a função de cada camada.
- **Racionalização:** A escolha por RabbitMQ e Docker foi orientada para garantir escalabilidade e manutenção simplificada, enquanto a organização por camadas (Data Warehouse e DB Gold) assegura a integridade e o desempenho dos dados.

---

### 5. Discussão em Sala de Aula (Obrigatório)
- **Apresentação realizada em sala:** A arquitetura foi apresentada e discutida em sala de aula.
- **Discussão intragrupo:** Foram analisadas diferentes abordagens antes de consolidar o modelo atual.
- **Feedback recebido:** O feedback foi utilizado para refinar as justificativas e o desenho da arquitetura.

---

### Observações
- **Escalabilidade garantida:** O uso de Docker permite escalar facilmente cada componente, ajustando a infraestrutura de acordo com a demanda.
- **Segurança e isolamento:** Containers fornecem isolamento para cada componente, minimizando riscos de interferência entre serviços.
- **Automatização de tarefas:** Os jobs periódicos no DB Gold asseguram a manutenção contínua e a consistência dos dados.
