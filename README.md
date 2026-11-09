# 📊 Social Media Data Audit Pipeline

Um sistema autônomo e resiliente, desenvolvido em **Node.js** e operado em **Docker**, projetado para extrair, estruturar e auditar dados massivos de redes sociais, garantindo integridade, deduplicação e armazenamento seguro em bancos relacionais.

## 🎯 O Problema
A extração de grandes volumes de dados não-estruturados (como comentários e respostas em redes sociais) costuma falhar por limites de paginação ou perda de conexão. O desafio era criar um coletor próprio que superasse as limitações de ferramentas de mercado (como a HikerAPI), preservasse os dados e oferecesse um painel analítico para auditoria.

## 🏗️ Arquitetura e Solução Técnica (Data Engineering)
A solução foi arquitetada focando em resiliência, validação contínua (Checkpoints) e governança de dados.

*   **Stack Backend/Coleta:** Node.js, Playwright, Chromium, hospedado em container Docker (Oracle Cloud).
*   **Stack Frontend/Auditoria:** Painel de gestão desenvolvido com integração nativa ao Supabase.
*   **Gestão de Dados:** Supabase (PostgreSQL) atuando como *Data Warehouse*, armazenando dados brutos e relacionais.
*   **O Fluxo de Coleta:**
    1.  **Varredura Remota:** O Playwright consulta as páginas via acesso remoto autenticado (noVNC), evitando bloqueios de *headless browsers*.
    2.  **Gravação Contínua (Checkpoints):** Gravação de cursor e hashes de integridade, permitindo retomada exata em caso de falha.
    3.  **Deduplicação:** União de passagens independentes, preservando apenas comentários exclusivos.

## 📈 Impacto e Capacidade Comprovada
O painel de auditoria abaixo demonstra a escala do processamento de dados (mais de 96 mil comentários indexados e categorizados):

*(Adicione aqui a imagem do seu Dashboard de Início, substituindo a URL abaixo pelo link gerado pelo GitHub após o upload)*
`![Dashboard de Auditoria](COLE_AQUI_O_LINK_DA_IMAGEM_DO_DASHBOARD)`

## 🔍 Funcionalidades de Auditoria e Governança

### Cruzamento Relacional (Autores e Expressões)
O sistema não apenas coleta, mas estrutura os dados. É possível buscar ocorrências por autor, perfil, identificar comentários excluídos (tracking de indisponíveis) e reconstruir a árvore de conversas preservando o contexto original.

*(Adicione aqui a imagem do Explorador ou de Autores)*
`![Exploração de Dados](COLE_AQUI_O_LINK_DA_IMAGEM_DO_EXPLORADOR)`

### Exportação com Criptografia (SHA-256)
Para uso em análises acadêmicas ou jurídicas, a plataforma garante a imutabilidade dos dados, exportando os lotes com registro de hash SHA-256, suportando múltiplos formatos (.xlsx, CSV, Parquet) e sorteios reprodutíveis.

*(Adicione aqui a imagem da tela de Exportação)*
`![Painel de Exportação e Hash](COLE_AQUI_O_LINK_DA_IMAGEM_DE_EXPORTACAO)`
