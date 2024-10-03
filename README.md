# Relatório Power BI - Análise de Vendas

Este relatório de vendas em **Power BI** foi desenvolvido com o objetivo de fornecer uma visão detalhada sobre o desempenho de produtos, localização dos clientes, receita mensal, e análise por faixa etária. O relatório inclui 3 abas principais e botões de navegação para facilitar a interação com as diferentes visualizações.


## Navegação no Relatório
O relatório possui **3 abas** principais, com botões para facilitar a navegação:
- Na aba **Home**, há dois botões:
  1. **Dashboard**: Ao clicar, você será direcionado para a visão detalhada geral (Dashboard).
  2. **Mapa Mundial**: Redireciona para a aba que contém a visão por estado no mapa.

Nas abas do **Dashboard** e do **Mapa**, há também um botão para voltar à página principal (Home).

> **Nota**: Como o arquivo é **.pbix** (editável), os botões só funcionam corretamente se o botão **CTRL** estiver pressionado ao clicar.

## Tratamento dos Dados
Na tabela **Vendas_Tratadas**, os seguintes tratamentos foram realizados:
- Alteração do tipo de cada coluna para atender às necessidades do projeto, como número inteiro, decimal, moeda (Real - Brasil), data, etc.
- Criação de uma nova coluna para trazer o **mês nominal** (nome do mês) que não existia nos dados.
- Todos os nomes de campos e valores foram ajustados para **maiúsculas** para padronização e consistência.

## Visualizações

### Receita Mensal
A visualização de **Receita Mensal** exibe os dados dos últimos 6 meses de cada ano, considerando a última data presente na base de dados. 
- Para criar essa visualização, foi criada uma fórmula que separa as vendas em "Últimos 6 meses" ou "Mais de 6 meses", permitindo uma visão anual e filtrada.
- Essa fórmula está na tabela **Vendas_Tratadas** com o nome **Ultimos_6_Meses**.
- Os nomes dos produtos foram ajustados para uma melhor visualização. Antes, eram identificados apenas por números (1, 2, 3...), então foi adicionado o prefixo "Produto", ficando assim: **Produto 1**, **Produto 2**, etc.

### 5 Produtos Mais Vendidos
A visualização dos **5 produtos mais vendidos** foi configurada para **remover a interação com o filtro de produto**, já que o gráfico já apresenta os 5 melhores produtos, não necessitando de filtragem adicional.

### Receita por Localização
Percebi que a **localidade dos clientes** estava trazendo dados incorretos (como sobrenomes). Para resolver isso:
- Criei uma nova tabela associando a **VendaID** a uma cidade e estado aleatórios. Isso resultou em uma tabela com **1000 cidades**.
  - Exemplo: A **VendaID 1** é associada à cidade de **Vila Velha** (ES), e a **VendaID 2** a **Maceió** (AL).
- Foi criada uma relação entre a **VendaID** da tabela **Cidades_Estados** e a tabela **Vendas_Tratadas**.
- Na coluna **NomeCompletoEstado**, o nome da cidade e do estado são exibidos juntos, mas foi criada uma medida para extrair apenas o nome do estado quando necessário.
- Também foi adicionado um **cartão** para exibir o nome do estado e cidade filtrados. Uma medida chamada **EstadoFiltrado** foi criada para garantir que, quando nenhuma cidade estiver selecionada, o cartão fique invisível.

### Faixa Etária
Foi criada uma definição das **faixas etárias** com base na idade dos clientes, utilizando a seguinte lógica:
- [Idade] <= 18: "Até 18"
- [Idade] <= 30: "19-30"
- [Idade] <= 40: "31-40"
- [Idade] <= 50: "41-50"
- [Idade] <= 60: "51-60"
- "Acima de 60"

Se for necessário alterar as faixas, a fórmula deverá ser ajustada conforme o novo critério.

### Ajustes para Visualização por Mês
Para que a visualização por **mês** seja cronológica (e não alfabética), foi necessário transformar a **DataVenda** em uma coluna que extraísse o **mês nominal** (ex: Janeiro) e o **número do mês** (ex: 1). Com isso, o filtro de mês funciona corretamente na ordem cronológica.

## Mapa por Estado
Criei uma segunda aba com um **mapa por estado**, que apresenta uma visão geográfica das vendas.
- Foi necessário criar uma coluna com o **nome completo do estado** e categorizar como **Estado ou Província** para que o mapa funcione corretamente.
- Existem dois **cartões** na página:
  1. **Valor Total das Vendas**
  2. **Quantidade de Vendas**

Se o estado não for corretamente categorizado, o Power BI pode exibir valores em outros países devido à abreviação de estados.

## Conclusão
Este relatório oferece uma visão ampla e detalhada sobre o desempenho de vendas, produtos, localização dos clientes e análise demográfica por faixa etária. A organização dos dados e as visualizações criadas foram otimizadas para facilitar a navegação e o entendimento das informações.

As funcionalidades de navegação e filtros permitem que os usuários interajam com o relatório de maneira intuitiva, ajustando as visualizações conforme necessário.
