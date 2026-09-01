# SalesInsight PY

## Sobre o projeto

O **SalesInsight PY** é um projeto de análise e visualização de dados de vendas desenvolvido em Python como parte do Mini-Projeto do Módulo 01.

O projeto implementa um fluxo completo de análise de dados, envolvendo:

- carregamento e inspeção dos dados;
- limpeza e tratamento de inconsistências;
- transformação dos dados;
- criação de colunas derivadas;
- cálculo de métricas agregadas;
- segmentação de clientes;
- operações numéricas com NumPy;
- geração de visualizações;
- exportação dos resultados em CSV, JSON e PNG.

O objetivo é transformar um dataset bruto de vendas em informações organizadas que possam auxiliar na compreensão do desempenho comercial da empresa.

**Repositório:** https://github.com/gniederle/mini-projeto-salesinsight-py

**Kanban:** https://github.com/users/gniederle/projects/1/views/1

---

## O que o projeto analisa

O projeto busca responder as seguintes questões:

- Como as vendas se comportam ao longo do tempo?
- Quais meses apresentam maior receita?
- Quais produtos geram mais receita?
- Quais categorias possuem melhor desempenho?
- Quais regiões apresentam maior receita?
- Quais clientes possuem maior gasto acumulado?
- Como os clientes se distribuem entre os segmentos Bronze, Prata e Ouro?
- Existe relação entre a quantidade vendida e a receita gerada por transação?

### Principais análises

- Receita total, quantidade vendida e número de vendas por mês;
- Receita por produto, com destaque para os 5 produtos de maior receita;
- Receita por categoria;
- Receita total e ticket médio por região;
- Segmentação de clientes por nível de gasto:
  - **Bronze:** abaixo de R$ 5.000,00;
  - **Prata:** de R$ 5.000,00 a R$ 15.000,00;
  - **Ouro:** acima de R$ 15.000,00;
- Operações vetorizadas utilizando NumPy;
- Relação entre quantidade vendida e receita por transação.

---

## Organização do código

Pela falta de familiaridade com o colab, cada etapa do projeto foi implementada de formas diferentesUma das principais decisões do projeto foi dividir o processamento em funções com responsabilidades específicas.

Em vez de concentrar todo o processamento em uma única função ou bloco de código, cada etapa possui uma responsabilidade própria.

Essa organização foi adotada para:

- melhorar a legibilidade;
- facilitar a manutenção;
- reduzir a complexidade de cada função;
- permitir o reaproveitamento das funções;
- facilitar a identificação e correção de erros;
- aproximar o projeto de uma estrutura de pipeline reutilizável.

O projeto também possui uma classe responsável por encapsular o fluxo de análise, permitindo manter o estado dos dados e reutilizar as funções desenvolvidas.

---

## Decisões técnicas

### Limpeza dos dados

Os registros com datas inválidas foram removidos após a conversão utilizando `pd.to_datetime(..., errors="coerce")`.

Também foram removidos registros com valores nulos nas colunas críticas `quantidade` e `preco_unitario`.

A decisão de remover esses registros foi tomada porque essas informações são necessárias para calcular a receita das transações. A imputação de valores não foi utilizada, pois essa estratégia é arriscada e foi desconsiderado nesse trabalho.

### Padronização dos clientes

Os nomes dos clientes foram tratados utilizando expressões regulares (`re`), removendo caracteres não alfanuméricos e padronizando os identificadores no formato:

```text
Cliente_NNN
```

Também foi criada uma indicação para identificar registros que estavam originalmente fora do padrão esperado.

### Transformações condicionais

A classificação da receita por transação utiliza `np.select()` em vez de estruturas de repetição. Essa escolha permite realizar a classificação de forma vetorizada, mantendo o código mais conciso e aproveitando os recursos do NumPy.

### Funções de ordem superior

Foi criada uma função capaz de receber outra função como argumento e aplicá-la a uma coluna do DataFrame.

Essa abordagem demonstra o conceito de funções como objetos e permite reutilizar a mesma estrutura para diferentes transformações.

### Classe

Foi criada a classe `SalesDataAnalyzer` para encapsular o fluxo de análise.

A classe mantém como atributos o DataFrame bruto, o DataFrame limpo, as métricas, a segmentação de clientes, as estatísticas NumPy e o relatório de limpeza.

Os métodos da classe reutilizam as funções desenvolvidas nas etapas anteriores.

---

## Visualizações

O projeto gera quatro figuras principais:

### 1. Receita por mês

Gráfico de linha apresentando a evolução da receita total ao longo dos meses.

### 2. Top 5 produtos

Gráfico de barras apresentando os cinco produtos com maior receita.

### 3. Quantidade vs Receita

Gráfico de dispersão relacionando a quantidade vendida com a receita de cada transação, diferenciando as categorias.

### 4. Painel resumo

Figura composta por quatro subplots, reunindo:

- receita por mês;
- Top 5 produtos;
- quantidade vs receita;
- receita por região.

Os gráficos são exportados no formato PNG.

---

## Arquivos gerados

Após a execução do projeto, os resultados são organizados no diretório `outputs/`:

```text
outputs/
├── metricas_por_mes.csv
├── segmentacao_clientes.csv
├── estatisticas_gerais.json
└── graficos/
    ├── receita_por_mes.png
    ├── top_produtos.png
    ├── quantidade_vs_receita.png
    └── painel_resumo.png
```

---

## Como executar

### Google Colab

O projeto foi desenvolvido utilizando o Google Colab.

1. Abra o notebook `salesinsight.ipynb` no Google Colab.
2. Faça o upload do arquivo `vendas.csv`.
3. Execute as células do notebook na ordem apresentada.
4. Ao final, os resultados serão exibidos no notebook e os arquivos serão exportados para o diretório `outputs/`.

O fluxo completo também possui uma função `main()` responsável por executar as etapas na ordem correta.

O projeto conta com a pasta utils na qual contém o script para gerar um novo CSV caso necessário.

---

## Organização do Kanban

O Kanban foi organizado de acordo com os requisitos definidos no documento do mini-projeto.

Cada requisito foi transformado em uma tarefa, permitindo acompanhar a implementação de cada etapa do projeto de forma organizada. Dessa forma, cada bloco do colab é referente a um requisito.

Além disso, cada tarefa do Kanban possui seu respectivo Merge Request, permitindo relacionar a implementação realizada com a tarefa correspondente.

Essa organização foi utilizada para facilitar o acompanhamento do desenvolvimento, revisão das alterações e controle das versões do projeto.

**Kanban do projeto:** https://github.com/users/gniederle/projects/1/views/1

---

## Versionamento

**Repositório:** https://github.com/gniederle/mini-projeto-salesinsight-py

---

## Considerações finais

O projeto foi desenvolvido com foco não apenas na obtenção dos resultados, mas também na organização do código e na aplicação prática dos conceitos apresentados no Módulo 01.

A divisão do fluxo em funções, a utilização de uma classe, o versionamento das alterações e a organização das tarefas no Kanban foram adotados para tornar o desenvolvimento mais estruturado, legível e próximo de um fluxo de trabalho utilizado em projetos reais de análise de dados.

---

## Vídeo de demonstração

Não foi possível fazer o video por falta de tempo (talvez será entregue com atraso).
