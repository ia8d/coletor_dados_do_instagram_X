# 📊 Social Media Audit Pipeline (OSINT & NLP Data Collector)

Um *case* de Engenharia de Dados focado em **Continuidade de Pesquisa Científica (Disaster Recovery)**. Este repositório documenta uma infraestrutura interna de coleta, armazenamento e auditoria de dados de redes sociais, desenvolvida como plano de contingência para viabilizar uma pesquisa de **Doutorado em Sociologia**.

## 🌐 O Contexto e o Desafio Científico
O projeto visa coletar e estruturar uma base projetada em **mais de 500.000 comentários e respostas** de perfis parlamentares no Instagram e X (Twitter). 

O objetivo analítico é alimentar modelos de processamento de linguagem natural (NLP) para mapear a **Violência Política de Gênero**, classificando comentários ofensivos e comparando a volumetria e o tom das ameaças direcionadas a candidatos homens versus candidatas mulheres. 

Para a pesquisa acadêmica ter validade, a integridade dos dados coletados precisa ser absoluta. Quando a API terceirizada que utilizávamos (HikerAPI) apresentou falhas críticas de paginação e perda silenciosa de dados, a tese correu risco. 

## 🛠️ A Ação de Contingência (In-House Pipeline)
Para garantir o rigor metodológico e não perder dados vitais, construímos rapidamente um pipeline próprio de extração e auditoria.

*   **Stack de Extração (Backend):** Node.js, Playwright e Chromium operando dentro de um container Docker (Oracle Cloud).
*   **Resiliência (Big Data):** Sistema de Checkpoints com gravação de cursor. Com uma volumetria projetada superior a meio milhão de registros, o robô foi arquitetado para retomar a extração exatamente do último ponto em caso de queda de conexão, sem duplicar dados.
*   **Gestão de Dados:** Supabase (PostgreSQL) atuando como *Data Warehouse* seguro para a estruturação relacional.

## 📈 Escala da Operação (Dashboard)
Durante a janela de contingência, o sistema orquestrou a captura e a auditoria em alta escala. O painel abaixo ilustra um recorte da volumetria estruturada (centenas de milhares de interações indexadas):

*(Adicione aqui a imagem do seu Dashboard de Início)*
`![Dashboard de Auditoria](COLE_AQUI_O_LINK_DA_IMAGEM_DO_DASHBOARD)`

## 🔍 Rigor Metodológico e Governança

### Reconstrução de Contexto (Fios de Conversa)
Para classificar ameaças com precisão, o modelo precisa de contexto. O sistema reconstrói a árvore de comentários (identificando autores cruzados entre plataformas e *parent_ids*), permitindo analisar o gatilho de uma ofensa, mesmo que o post original seja apagado.

*(Adicione aqui a imagem do Explorador de Posts ou Autores)*
`![Exploração de Dados](COLE_AQUI_O_LINK_DA_IMAGEM_DO_EXPLORADOR)`

### Cadeia de Custódia e Exportação (SHA-256)
A validade de um Doutorado exige prova de que os dados não foram manipulados. O sistema conta com um módulo de exportação (.xlsx, CSV) que gera e registra um hash SHA-256 para cada lote, garantindo imutabilidade criptográfica para auditoria acadêmica.

*(Adicione aqui a imagem da tela de Exportação)*
`![Painel de Exportação e Hash](COLE_AQUI_O_LINK_DA_IMAGEM_DE_EXPORTACAO)`

## 🏁 Desfecho e Maturidade de Software
Durante a operação, documentamos as falhas e acionamos o suporte técnico da HikerAPI. Após a correção estrutural pelo fornecedor, **descontinuamos o uso deste scraper customizado**. Esta decisão reflete maturidade executiva: evitamos o "Not Invented Here" (Síndrome do Não Inventado Aqui) e eliminamos débito técnico interno, comprovando a capacidade de construir soluções complexas sob demanda, mas mantendo a operação *Lean* ao retornar à API estabilizada.
