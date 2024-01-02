# Além de "Você Também Pode Gostar": Desconstruindo Escolhas do Consumidor com Ciência de Dados

Este projeto de Ciência de Dados apresenta uma abordagem baseada em dados para entender o comportamento do consumidor e personalizar recomendações de produtos usando um conjunto de dados da e-commerce britânica **Rex London**. A fim de impulsionar significativamente as vendas e aprimorar a experiência do cliente, projeto está estruturado em torno de três capítulos principais: **Análise Exploratória de Dados**, **Análise de Cesta de Mercado** e **Sistema de Recomendação**.

# Sobre a Rex London
Rex London é um varejista de comércio eletrônico com sede no Reino Unido que oferece uma gama diversificada de produtos, como presentes e acessórios para casa. A empresa quer aumentar o engajamento com os visitantes da página e melhorar a experiência de compra dos clientes.

# O problema de negócio
Para alcançar os objetivos acima, a empresa precisa entender quais são os produtos que normalmente são comprados juntos e construir um sistema de recomendação de produtos com base no perfil dos seus clientes.

# Solução do problema
- O projeto começa a partir da Análise Exploratória de Dados (EDA), etapa crucial para descobrir padrões ocultos em compras, como comportamento do consumidor, preferências de produtos, tamanho da cesta e preços médios ao longo do tempo.

- A EDA abre caminho para as *regras de associação* usadas em uma **Análise de Cesta de Mercado** com a biblioteca `apriori` em Python. Mais do que apenas usar a biblioteca, termos-chave como **antecedentes**, **consequentes**, **suporte**, **confiança** e **lift** também são explicados.

- Além disso, é desenvolvido um **sistema de recomendação** baseado na semelhança entre clientes para gerar recomendações de produtos. Assim, à medida que os clientes navegam pelo site, sua experiência é personalizada para prever o que *"eles também podem gostar"* e maximizar as vendas para a empresa.

# Análise Exploratória de Dados

### Como é a distribuição de compras em 2011?
![image](https://github.com/caiocasagrande/customer_behavior/blob/main/images/3_2_purchases_per_day_2011.png)
- Os dados estão mais comportados em 2011 do que em 2010, mas as variações são muito expressivas
- Existem um pouco mais de 10 picos nas compras de 2011

### Qual é a relação entre preço e quantidade? Quanto maior o preço, menor a quantidade?
![image](https://github.com/caiocasagrande/customer_behavior/blob/main/images/3_8_avg_price_vs_avg_qnt.png)
- A relação entre preço e quantidade é inversamente proporcional
- O preço médio é maior para itens com uma quantidade menor
- O preço médio é menor para itens com uma quantidade maior
- Portanto, quanto maior o preço, menor a quantidade

### Qual é o comportamento do *preço* e *tamanho* das cestas por mês em 2011?
![image](https://github.com/caiocasagrande/customer_behavior/blob/main/images/3_10_avg_price_avg_size_basket_per_month.png)
- O preço médio das cestas atinge o ponto mais baixo em junho, seguido por julho
- Os preços médios mais altos das cestas são observados de setembro a novembro
- Setembro e outubro também são os meses com o maior tamanho médio de cestas
- **Levando também em consideração o número de compras por mês visto anteriormente, podemos afirmar que o final do ano é o melhor momento para a empresa vender seus produtos**

# Market Basket Analysis 

## Market Basket Analysis Results

<div align="center">
  
| antecedents                                            | consequents                    | support | confidence | lift   |
|--------------------------------------------------------|--------------------------------|---------|------------|--------|
| GREEN REGENCY TEACUP AND... | ROSES REGENCY TEACUP AND S... | 0.019   | 0.828      | 16.296 |
| LUNCH BAG WOODLAND... | LUNCH BAG RED RETROSPOT       | 0.011   | 0.826      | 9.641  |
| STRAWBERRY CHARLOTTE BAG... | RED RETROSPOT CHARLOTTE BAG    | 0.012   | 0.821      | 17.765 |
| LUNCH BAG PINK POLKADOT... | LUNCH BAG BLACK SKULL         | 0.010   | 0.798      | 10.523 |
| LUNCH BAG WOODLAND... | LUNCH BAG RED RETROSPOT       | 0.011   | 0.797      | 9.296  |
| JUMBO BAG VINTAGE LEAF...| JUMBO BAG RED RETROSPOT       | 0.012   | 0.796      | 7.551  |
| LUNCH BAG WOODLAND, BAG... | LUNCH BAG RED RETROSPOT       | 0.011   | 0.789      | 9.203  |
| JUMBO BAG PEARS, JUMBO...   | JUMBO BAG APPLES              | 0.011   | 0.788      | 16.106 |
| JUMBO BAG SCANDINAVIAN... | JUMBO BAG RED RETROSPOT       | 0.011   | 0.785      | 7.447  |
| GREEN REGENCY TEACUP...            | ROSES REGENCY TEACUP AND S... | 0.036   | 0.779      | 15.334 |

</div>

### Explaining the terms

- **Antecedents:** These are the items that are the starting point for the analysis. In other words, they are present in the basket before the consequent item is purchased.
- **Consequents:** These are the items that are likely to be purchased after the antecedents.
    - Associaton rule: If the *antecedents* are present in the basket, the *consequent* is likely to be purchased.
- **Support:** Support measures how frequently the items of a rule (both antecedents and consequents) appear together in the dataset. It is the proportion of transactions in which the items are bought together. 
- **Confidence:** This is a measure of the likelihood of the consequent item being purchased when the antecedent item is already in the basket. 
- **Lift:** Lift measures the degree of association between the antecedent and consequent items, while considering the baseline purchase probability of the consequent item. A lift value greater than 1 indicates a positive association, meaning that the items are more likely to be bought together than independently.

# Recommendation System 
## Recommendation System Steps
1. Construct an utility matrix
- Utility matrix is a matrix that contains the number of times an item was purchased (`quantity`) by each client
2. Calculate the similarity between clients using *cosine similarity*
- Cosine similarity is a metric that measures the similarity between two vectors
3. Create a dataframe that contains the similarity matrix
- Clients as rows and columns with their similarity values in the matrix
4. Generate recommendations looping through each client 
- The goal is to recommend two products based on the three most similar clients
- Get the k most similar clients
- Get the products purchased by the similar clients
- We want only the products that have not been purchased
- Recommend the top n products that have not been purchased
5. Create a dataframe with the recommendations for each client

## Recommendation System Results

<div align="center">

| customer_id | product_1                          | product_2                                    |
|-------------|-----------------------------------|----------------------------------------------|
| 12347       | WRAP 50'S CHRISTMAS               | 10 COLOUR SPACEBOY PEN                       |
| 12349       | GIRLS VINTAGE TIN SEASIDE BUCKET  | RED RETROSPOT WRAP                            |
| 12350       | BLACK STITCHED WALL CLOCK          | PACK OF 12 LONDON TISSUES                    |
| 12352       | WALL TIDY RETROSPOT                | CERAMIC BOWL WITH LOVE HEART DESIGN          |
| 12353       | HANGING HEART MIRROR DECORATION    | MINI CAKE STAND T-LIGHT HOLDER               |
| 12354       | JUMBO BAG PINK VINTAGE PAISLEY     | JUMBO BAG RED RETROSPOT                      |
| 12355       | WHITE SAGE INCENSE                 | COLOURED GLASS STAR T-LIGHT HOLDER           |
| 12356       | STRAWBERRY CERAMIC TRINKET POT     | SET 20 NAPKINS FAIRY CAKES DESIGN            |
| 12357       | HAND WARMER BIRD DESIGN            | PLASTERS IN TIN VINTAGE PAISLEY              |
| 12358       | BLACK/BLUE POLKADOT UMBRELLA        | RED RETROSPOT UMBRELLA                       |
| 12360       | GINGERBREAD MAN COOKIE CUTTER      | CHILDREN'S APRON DOLLY GIRL                  |
| 12361       | LUNCH BOX I LOVE LONDON            | LUNCH BAG PINK POLKADOT                      |
| 12362       | SPACEBOY GIFT WRAP                 | FOLKART STAR CHRISTMAS DECORATIONS          |
| 12363       | RED RETROSPOT TAPE                 | SET 40 HEART SHAPE PETIT FOUR CASES          |
| 12364       | MAGIC DRAWING SLATE SPACEBOY       | BIRTHDAY BANQUET GIFT WRAP                   |

</div>
