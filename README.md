#Dashboard de Chamados Oracle | Programa Conecta

Painel web para acompanhar chamados de suporte Oracle do Programa Conecta — Grupo Pluma. O projeto organiza os registros por ano e apresenta listas, indicadores, gráficos e rankings a partir de arquivos CSV exportados da operação.

Escopo: aplicação estática em HTML, CSS e JavaScript. Os dados são lidos pelo navegador; não há integração direta com a API da Oracle, banco de dados ou autenticação implementada nos arquivos deste projeto.

Funcionalidades

Visão anual: navegação entre os painéis de 2025 e 2026.

Lista de chamados: consulta por número da SR (Service Request, solicitação de serviço), serviço, tipo, status, severidade, datas e contato primário.

Indicadores: total de chamados, abertos, fechados e serviço com maior volume.

Filtros e busca: seleção por serviço, status e severidade, além de pesquisa textual na lista.

Gráficos: distribuição por mês, serviço, tipo de ocorrência e severidade; comparativo anual de abertos e fechados.

Rankings: dez serviços e dez contatos primários com mais chamados.

Leitura alternativa: algumas páginas permitem selecionar manualmente um CSV quando a carga automática falha.

Modo TV: visualização em tela cheia na lista de chamados.

Tecnologias

Camada

Tecnologia

Interface

HTML5, CSS3, JavaScript e Bootstrap 5.3.3

Gráficos

Chart.js e chartjs-plugin-datalabels

Dados

Arquivos CSV carregados com fetch

Hospedagem

Servidor HTTP estático, incluindo GitHub Pages

As bibliotecas visuais são carregadas por CDN (rede de distribuição de conteúdo); para exibir corretamente a interface e os gráficos, o navegador precisa conseguir acessá-las.

Estrutura do projeto

.
├── index.html                    # Página inicial e comparativo anual
├── principal.js                  # Navegação e comparativo de 2025 × 2026
├── estilo.css                    # Estilos compartilhados
├── index_2025.html / .js         # Lista e indicadores de 2025
├── index_2026.html / .js         # Lista e indicadores de 2026
├── graficos_2025.html / .js      # Gráficos de 2025
├── graficos_2026.html            # Gráficos de 2026
├── graficos_2026_v2.js           # Script carregado por graficos_2026.html
├── top-modulos_2025.html / .js   # Ranking de serviços de 2025
├── top-modulos_2026.html / .js   # Ranking de serviços de 2026
├── top-contatos_2025.html / .js  # Ranking de contatos de 2025
├── top-contatos_2026.html / .js  # Ranking de contatos de 2026
├── dados_sr_2025.csv             # Exportação exigida pelas páginas de 2025
├── dados_sr_2026.csv             # Exportação exigida pelas páginas de 2026
└── logo-conecta.png              # Imagem referenciada pelos cabeçalhos

Os nomes do diagrama representam os caminhos esperados pelo código, não a confirmação de que todos esses arquivos foram enviados. Há também páginas e scripts sem sufixo de ano nos arquivos analisados, que parecem versões anteriores; mantenha os conjuntos anuais acima como referência para a publicação.

Como executar

Coloque as páginas HTML, os scripts JavaScript, estilo.css, os CSVs anuais e o logotipo na mesma pasta, preservando exatamente os nomes referenciados nos arquivos HTML e JavaScript.

Na pasta do projeto, inicie um servidor local:

python -m http.server 8000

Abra http://localhost:8000 no navegador.

Abrir index.html diretamente com file:// pode impedir a carga automática dos CSVs pelo navegador. Nas páginas que oferecem seleção manual de arquivo, esse controle pode ser usado como alternativa.

Preparação dos dados

Os scripts procuram dados_sr_2025.csv e dados_sr_2026.csv na pasta das páginas. O conjunto de arquivos analisado contém somente dados_sr.csv, com 73 registros e campo Gerado_em de 2025. Para testar os painéis de 2025, copie esse arquivo como dados_sr_2025.csv. Para habilitar 2026 e o comparativo na página inicial, adicione uma exportação própria de 2026 como dados_sr_2026.csv.

O cabeçalho esperado é:

Número SR,Serviço,Issue Type,Status,Severidade,Criado_dt,Atualizado_dt,Contato Primário,Gerado_em

Use CSV em UTF-8, com vírgula como separador e nomes de colunas preservados. Se um campo contiver vírgula, coloque-o entre aspas conforme o padrão CSV. Os rankings dependem especialmente de Serviço e Contato Primário; os gráficos mensais dependem das datas. Os dados exibidos refletem o conteúdo do arquivo carregado, não uma atualização automática da Oracle.

Publicação no GitHub Pages

Envie os arquivos para a raiz do repositório, preservando seus nomes e letras maiúsculas/minúsculas.

Em Settings → Pages, selecione Deploy from a branch, a branch desejada e a pasta / (root).

Ao publicar, confira o carregamento de index.html, dos dois CSVs anuais e dos recursos visuais.

Para atualizar o painel, substitua o CSV do ano correspondente e publique a alteração. Antes de disponibilizar o repositório publicamente, revise os dados: os CSVs podem conter números de chamados e nomes de contatos, que ficarão acessíveis a quem puder acessar o site.

Pontos de atenção identificados

logo-conecta.png é referenciado nas páginas, mas não estava entre os arquivos recebidos. Inclua a imagem para evitar o logotipo quebrado.

O arquivo adicional graficos.html referencia graficos.js, que não estava entre os arquivos recebidos. Use graficos_2025.html e graficos_2026.html para as visões anuais, ou ajuste essa página antiga antes de publicá-la.

A classificação de “aberto” e “fechado” é calculada a partir do texto em Status; alguns scripts consideram valores ligeiramente diferentes. Padronize essa regra caso os números precisem servir como indicador oficial.

A leitura dos CSVs é feita por scripts próprios em diferentes páginas. Antes de alterar o layout da exportação, valide lista, gráficos, rankings e comparativo anual.

Não foi identificado arquivo de licença nos materiais analisados. Defina uma licença antes de permitir reutilização externa do código.

Manutenção

Para acrescentar outro ano, duplique as páginas e scripts anuais, atualize as referências ao novo dados_sr_<ano>.csv e inclua os links na página inicial. Para alterar a regra de status ou o formato do CSV, revise todos os scripts que fazem a leitura desses dados, inclusive principal.js.
