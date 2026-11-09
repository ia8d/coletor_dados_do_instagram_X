# 📊 Social Media Audit Pipeline (Contingency Scraper)

Um *case* de Engenharia de Dados focado em **Continuidade de Negócio (Disaster Recovery)**. Este repositório documenta uma infraestrutura interna de coleta, armazenamento e auditoria de dados de redes sociais (OSINT) desenvolvida como plano de contingência durante a falha de um fornecedor terceirizado.

## 🌐 O Contexto e o Incidente
Durante uma operação crítica de auditoria de dados públicos (cruzamento massivo de comentários e perfis parlamentares no Instagram e X), a API comercial que utilizávamos (HikerAPI) apresentou uma falha silenciosa, deixando de retornar blocos inteiros de dados e quebrando a paginação. 

Para não paralisar a pesquisa e não perder o *timing* da coleta de dados, a equipe precisava de uma solução imediata.

## 🛠️ A Ação de Contingência (In-House Pipeline)
Construímos e implementamos rapidamente um pipeline próprio de extração para contornar o bug da API terceirizada, reduzindo custos emergenciais e garantindo a continuidade do fluxo de dados.

*   **Stack de Extração (Backend):** Node.js, Playwright e Chromium operando dentro de um container Docker (Oracle Cloud).
*   **Gestão de Estado e Resiliência:** Sistema de Checkpoints com gravação de hashes de integridade. Se a conexão caísse, o robô retomava exatamente do último comentário.
*   **Gestão de Dados:** Supabase (PostgreSQL) atuando como *Data Warehouse* seguro para a estruturação relacional.
*   **Deduplicação Inteligente:** Tratamento direto no banco de dados para evitar inserção de comentários repetidos durante as varreduras de segurança.

## 📈 Resultados da Operação de Contingência
Durante o período em que operou, a ferramenta absorveu a carga massiva com sucesso. O dashboard interno abaixo ilustra o volume processado (mais de 96 mil comentários validados):

*(Adicione aqui a imagem do seu Dashboard de Início)*
`![Dashboard de Auditoria](COLE_AQUI_O_LINK_DA_IMAGEM_DO_DASHBOARD)`

## 🔍 Auditoria, Cruzamento e Governança

### Rastreador Relacional e Reconstrução de Fios
O sistema contornou as falhas da API cruzando dados entre plataformas e reconstruindo a árvore de comentários (identificando autores e *parent_ids*), o que permitiu recuperar o contexto das conversas e identificar postagens indisponíveis.

*(Adicione aqui a imagem do Explorador de Posts ou Autores)*
`![Exploração de Dados](COLE_AQUI_O_LINK_DA_IMAGEM_DO_EXPLORADOR)`

### Exportação Segura (SHA-256)
Para garantir que a coleta emergencial mantivesse validade analítica e de auditoria, o sistema exportava os pacotes em CSV/.xlsx com geração automática de hash SHA-256 (garantia de imutabilidade).

*(Adicione aqui a imagem da tela de Exportação)*
`![Painel de Exportação e Hash](COLE_AQUI_O_LINK_DA_IMAGEM_DE_EXPORTACAO)`

## 🏁 Desfecho e Maturidade de Software
Durante a operação da nossa ferramenta, documentamos os *logs* do erro e acionamos o suporte técnico da HikerAPI. Após a equipe deles corrigir a falha estrutural do lado do servidor, **descontinuamos o uso deste scraper customizado**. 

Esta decisão reflete uma cultura de **eliminação de débito técnico**: retornamos ao uso da API comercial estabilizada para manter a operação *Lean* (enxuta), comprovando a capacidade da equipe de construir soluções complexas sob demanda, mas mantendo a sabedoria de não manter código interno desnecessário quando o ecossistema terceirizado é normalizado.
