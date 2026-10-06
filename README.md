# Performance-de-entregas-e-satisfa-o-do-cliente
Dashboard em Power BI que investiga uma pergunta de negócio de e-commerce: pedidos entregues com atraso recebem notas piores dos clientes? Se sim, onde os atrasos se concentram e a partir de quantos dias a satisfação cai de forma mais forte?
Sumário
Objetivo
Dados
Como medi o atraso
Estrutura do relatório
Principais resultados
Recomendações
Limitações
Medidas DAX
Ferramentas
Autora
Objetivo
Responder, com dados, às perguntas abaixo:
Pedidos atrasados recebem notas piores?
Quantos pedidos atrasam e por quantos dias, em média?
A partir de quantos dias de atraso a satisfação cai de forma mais forte?
Em quais estados, vendedores e categorias o atraso se concentra?
Dados
Dataset público de e-commerce da Olist, disponível no Kaggle (Brazilian E-Commerce Public Dataset by Olist), com cerca de 99 mil pedidos. Tabelas utilizadas:
Tabela	Uso
`olist_orders_dataset`	Pedidos, datas de entrega e data estimada
`olist_order_items_dataset`	Itens do pedido e ligação com vendedor e produto
`olist_order_reviews_dataset`	Nota de avaliação do cliente
`olist_customers_dataset`	Estado do cliente
`olist_sellers_dataset`	Estado do vendedor
`olist_products_dataset` e `product_category_name_translation`	Categoria do produto
Os arquivos brutos não estão neste repositório. Para reproduzir o projeto, baixe o dataset no Kaggle e importe as tabelas no Power BI.
Como medi o atraso
Um pedido é considerado atrasado quando foi entregue depois da data estimada. Pedidos entregues após a previsão, mesmo no mesmo dia, foram contabilizados como 1 dia de atraso, para que atrasos de poucas horas não fossem classificados como zero.
Os atrasos foram agrupados em faixas: 1 dia, 2 a 3 dias, 4 a 7 dias e mais de 7 dias.
Estrutura do relatório
Página	Pergunta que responde
Pedidos	Qual o tamanho do problema e como a nota muda conforme o atraso?
Região	Em quais estados (do cliente) o atraso é mais frequente, mais longo e pior avaliado?
Vendedores	De quais estados (do vendedor) saem os pedidos atrasados?
Categoria	O atraso se concentra em algum tipo de produto?
![Página Região]
![Página Vendedores]
![Página Categoria]
Principais resultados
1. O atraso está associado a uma queda forte na satisfação
Situação	Nota média
Entregue no prazo	4,2
Entregue com atraso	2,5
A diferença é de 1,7 ponto. A nota média geral é 4,09.
2. Cerca de 1 em cada 11 entregas atrasa, e o atraso costuma ser longo
8,9% dos pedidos entregues chegaram depois da data estimada, o equivalente a cerca de 8,6 mil pedidos.
Entre os atrasados, o atraso médio foi de 16 dias. Muitos clientes receberam o pedido mais de duas semanas depois do prazo.
3. A satisfação cai mais entre 1 dia e 2 a 3 dias de atraso
Faixa de atraso	Nota média	Variação em relação à faixa anterior
No prazo	4,2	
1 dia	3,9	−0,3
2 a 3 dias	2,9	−1,0
4 a 7 dias	2,1	−0,8
Mais de 7 dias	1,7	−0,4
A maior queda acontece na passagem de 1 dia para 2 a 3 dias de atraso. A partir de 4 dias a nota já está abaixo de 2,5.
4. Volume e taxa de atraso apontam para estados diferentes
Considerando o estado do cliente:
Perspectiva	Estados	Leitura
Maior volume de atrasos	SP (2.672), RJ (1.783), MG (714), BA (483), RS (420)	Reflete o volume total de pedidos
Maior taxa de atraso	AL (24,94%), MA (21,06%), PI (17,23%), SE (16,42%), CE (16,03%)	Risco proporcional, todos bem acima da média de 8,9%
Menor nota média	RR (3,6), AL, MA, SE e PA (3,8)	Pior experiência percebida
Atrasos mais longos	RR (77 dias), AP (47), RO (37), AM (22), MT (21)	Maior gravidade quando o atraso acontece
Alagoas, Maranhão e Sergipe combinam alta taxa de atraso e baixa satisfação (nota média de 3,8). Roraima tem a menor nota (3,6) e o maior atraso médio, mas a amostra é pequena (veja Limitações).
5. Vendedores de São Paulo concentram o volume, mas não a taxa
Considerando o estado do vendedor, SP tem 6.365 pedidos atrasados e taxa de 9,27%, próxima da média geral. O volume alto vem da concentração de vendedores e pedidos no estado, e não de um desempenho pior. Já o Maranhão tem taxa de 23,14% (90 pedidos atrasados), bem acima da média.
6. O atraso não está concentrado em uma categoria específica
As categorias de maior volume (Cama, Mesa e Banho; Beleza e Saúde; Esporte e Lazer; Móveis e Decoração; Informática e Acessórios; Relógios e Presentes) têm taxas entre 8,2% e 9,5%, todas próximas da média. O atraso parece ser mais um problema logístico e regional do que de produto. Algumas categorias menores apresentam taxas mais altas, mas com volume baixo.
Recomendações
Criar alertas para pedidos com risco de atraso, já a partir de 1 dia de atraso projetado, porque é onde a nota mais cai.
Rever prazos prometidos e rotas no Nordeste (AL, MA, PI, SE e CE), onde a taxa de atraso é pelo menos o dobro da média.
Investigar a cobertura logística da região Norte (RR, AP e RO), onde os atrasos são mais longos. É preciso confirmar com mais dados, pela amostra reduzida.
Acompanhar SP e RJ pelo volume absoluto, pois pequenas melhorias de processo têm grande efeito em número de pedidos.
Aprofundar a análise por vendedor, para identificar casos individuais, já que a análise atual chega apenas ao estado.
Limitações
Associação não é causa. Os dados mostram que pedidos atrasados têm notas piores, mas outros fatores (qualidade do produto, frete, atendimento) também influenciam a nota.
Amostras pequenas distorcem taxas e médias. Estados e categorias com poucos pedidos (por exemplo, AM com 66,67% de atraso e Roraima com 77 dias de atraso médio) devem ser lidos com cautela. Os rankings do relatório aplicam um volume mínimo de pedidos para reduzir esse efeito.
Diferença entre totais. As páginas Vendedores e Categoria usam a tabela de itens e somam 8.368 pedidos atrasados (taxa de 8,67%), enquanto a página Pedidos soma cerca de 8,6 mil (8,9%). A diferença vem de pedidos sem correspondência na tabela de itens.
Estado do cliente x estado do vendedor. A página Região usa o estado do cliente (destino) e a página Vendedores usa o estado do vendedor (origem). Por isso os números de SP diferem entre elas.
A nota depende de quem avalia. Apenas pedidos com avaliação entram no cálculo da nota média.
Medidas DAX
Exemplos das principais medidas do modelo:
```dax
Pedidos Atrasados por Vendedor =
CALCULATE (
    DISTINCTCOUNT ( itens[order_id] ),
    pedidos[Status Entrega] = "Atrasado"
)

Pedidos Entregues por Vendedor =
CALCULATE (
    DISTINCTCOUNT ( itens[order_id] ),
    pedidos[Status Entrega] IN { "No prazo", "Atrasado" }
)

Taxa de Atraso por Origem do Vendedor =
DIVIDE (
    [Pedidos Atrasados por Vendedor],
    [Pedidos Entregues por Vendedor]
)
```
Ferramentas
Power BI Desktop
DAX
Modelagem de dados (relacionamentos entre pedidos, itens, clientes, vendedores, produtos e avaliações)
Autora
Michelly Fontoura, analista de dados.
