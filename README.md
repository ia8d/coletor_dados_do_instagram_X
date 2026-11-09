# 📊 Social Media Audit Pipeline (PROJETO EM ANDAMENTO)

Um *case* de Engenharia de Dados focado em **Continuidade de Pesquisa Científica**. Este repositório documenta uma infraestrutura interna de coleta, armazenamento e auditoria de dados de redes sociais, desenvolvida como plano de contingência para viabilizar uma pesquisa de **Doutorado em Sociologia**.

## 🌐 O Contexto e o Desafio Científico
O projeto visa coletar e estruturar uma base projetada em **mais de 500.000 comentários ,respostas e menções** de perfis parlamentares no Instagram e X (Twitter). 

O objetivo analítico é alimentar a base para mapear a **Violência Política de Gênero**. Para isso, integramos **Inteligência Artificial atuando como um filtro analítico autônomo**, processando o contexto massivo para classificar automaticamente comentários inofensivos versus discurso de ódio e ameaças direcionadas a candidatas e candidatos.

Para a pesquisa acadêmica ter validade, a integridade dos dados coletados precisa ser absoluta. Quando a API terceirizada que utilizávamos (HikerAPI) apresentou falhas críticas de paginação e perda silenciosa de dados, a tese correu risco. 

## 🛠️ A Ação de Contingência
Para garantir o rigor metodológico e não perder dados vitais, construímos rapidamente um pipeline próprio de extração e auditoria.

*   **Orquestração de Extração (n8n):** Todo o fluxo de requisições, controle de paginação, tratamento de erros e roteamento dos dados foi construído no **n8n**, garantindo uma governança visual e escalável do pipeline de mineração.
*   **Stack de Execução (Backend):** Node.js, Playwright e Chromium operando dentro de um container Docker (Oracle Cloud) para renderização e coleta nas camadas onde as APIs falham.
*   **Resiliência (Big Data):** Sistema de Checkpoints com gravação de cursor. Com uma volumetria projetada superior a meio milhão de registros, o robô retoma a extração exatamente do último ponto em caso de queda, sem duplicar dados no banco.
*   **Gestão de Dados:** Supabase (PostgreSQL) atuando como *Data Warehouse* seguro para a estruturação relacional.

## 📈 Escala da Operação 
Durante a janela de contingência, o n8n orquestrou a captura em alta escala. O painel abaixo ilustra um recorte da volumetria estruturada (centenas de milhares de interações indexadas para o filtro de IA):


**LINK DA IMAGEM:**
`https://raw.githubusercontent.com/ia8d/coletor_dados_do_instagram_X/refs/heads/main/dados2.PNG)`

## 🔍 Rigor Metodológico e Governança

### Inteligência Relacional e Contexto para a IA
Para classificar ameaças com precisão, a IA precisa de contexto completo. O sistema reconstrói a árvore de comentários (identificando autores cruzados entre plataformas e *parent_ids*), permitindo ao modelo de linguagem entender o gatilho exato de uma ofensa, mesmo que o post original tenha sido apagado.

**LINK DA IMAGEM:**
`https://github.com/ia8d/coletor_dados_do_instagram_X/blob/main/dados4.PNG?raw=true`

### Cadeia de Custódia e Exportação (SHA-256)
A validade de um Doutorado exige prova de que os dados não foram manipulados (seja por falha humana ou alucinação da IA). O sistema conta com um módulo de exportação (.xlsx, CSV) que gera e registra um hash SHA-256 para cada lote, garantindo imutabilidade criptográfica para auditoria acadêmica.

**LINK DA IMAGEM:**
`https://github.com/ia8d/coletor_dados_do_instagram_X/blob/main/dados1.PNG?raw=true`

## 🏁 Desfecho e Maturidade de Software

Durante a operação, documentamos as falhas e acionamos o suporte técnico da HikerAPI. Após a correção estrutural pelo fornecedor, **descontinuamos o uso deste pipeline customizado**. Esta decisão reflete maturidade executiva e eliminamos débito técnico interno, comprovando a capacidade de construir orquestrações complexas sob demanda, mas mantendo a operação rodando ao retornar à API estabilizada.
