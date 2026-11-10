📊 Coleta Parlamentar — Pipeline de Dados para Pesquisa Acadêmica

🚧 Projeto em andamento. Infraestrutura de dados desenvolvida para apoiar uma pesquisa de Doutorado em Sociologia sobre violência política de gênero nas redes sociais. Por se tratar de pesquisa não publicada, o código-fonte, ainda são privados. Este repositório documenta apenas a arquitetura e as decisões de engenharia.

🎯 O problema

A pesquisa precisa coletar posts, comentários, respostas e menções de perfis parlamentares no Instagram e no X (Twitter), em janelas de tempo definidas pela metodologia, e entregar esses dados às pesquisadoras de forma organizada, rastreável e auditável.

Durante a coleta, a API terceirizada que utilizávamos (HikerAPI) apresentou falhas de paginação e perda silenciosa de dados. Para uma tese, dado faltando sem aviso compromete a validade do estudo.

🛠️ O que eu construí
1. Coleta resiliente
Orquestração no n8n: requisições, paginação, tratamento de erros e roteamento dos dados.
Coleta com navegador automatizado: Node.js + Playwright + Chromium em container Docker (Oracle Cloud) para os pontos onde a API falhava.
Checkpoints com cursor: se a coleta cai, ela retoma do último ponto salvo, sem duplicar registros.
Banco: Supabase (PostgreSQL), modelando posts, comentários, respostas (com parent_id) e menções.
2. Painel para as pesquisadoras
Visão geral do andamento por janela de coleta (J1–J6 + janela extra) e por plataforma.
Perfis: indicadores por parlamentar (posts, comentários, respostas, menções), com filtro por gênero e pareamento.
Explorador de fios: leitura dos comentários em árvore (respeitando parent_id), com busca, filtros e anotações de campo registradas por usuário autenticado.
Pseudonimização: autores de comentários sempre exibidos como pseudônimo.
3. Rigor metodológico
Exportação em Excel (conversa, dados brutos, anotações e classificações) e CSV.
Hash SHA-256 por pacote exportado, registrado no banco: prova de que o arquivo analisado é o mesmo que foi gerado.
Amostragem reproduzível: sorteio com seed salva, permitindo reproduzir exatamente a mesma amostra depois.
Importação de codificação manual: as pesquisadoras classificam em planilha e o sistema importa e audita linhas inválidas.

A classificação dos comentários é feita manualmente pelas pesquisadoras (análise qualitativa). O papel do sistema é garantir que os dados cheguem completos, organizados e rastreáveis.

📈 Volume atual (recorte do X)
Métrica	Valor
Contas monitoradas	32
Posts coletados	~2,7 mil
Comentários e respostas	~96 mil
Menções	~18,8 mil
🧱 Stack

n8n · Node.js · Playwright · Docker · Oracle Cloud · Supabase (PostgreSQL) · <!-- TODO: stack do painel, ex.: React/Next.js -->

🧠 O que aprendi
Em pesquisa, dado faltando em silêncio é pior que erro explícito. Por isso checkpoints, auditoria de importação e hash.
Construir a contingência e depois voltar para a API quando o fornecedor corrigiu foi uma decisão de reduzir manutenção, não de abandonar o projeto.
