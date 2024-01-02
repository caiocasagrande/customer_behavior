# Além de "Você Também Pode Gostar": Desconstruindo Escolhas do Consumidor com Ciência de Dados

Este projeto de Ciência de Dados apresenta uma abordagem baseada em dados para entender o comportamento do consumidor e personalizar recomendações de produtos usando um conjunto de dados da e-commerce britânica **Rex London**. A fim de impulsionar significativamente as vendas e aprimorar a experiência do cliente, projeto está estruturado em torno de três capítulos principais: **Análise Exploratória de Dados**, **Análise de Cesta de Mercado** e **Sistema de Recomendação**.

## 1. Sobre a Rex London
Rex London é um varejista de comércio eletrônico com sede no Reino Unido que oferece uma gama diversificada de produtos, como presentes e acessórios para casa. A empresa quer aumentar o engajamento com os visitantes da página e melhorar a experiência de compra dos clientes.

Os dados foram obtidos através da plataforma [Kaggle](https://www.kaggle.com/datasets/aslanahmedov/market-basket-analysis).

## 2. O problema de negócio
Para alcançar os objetivos acima, a empresa precisa entender quais são os produtos que normalmente são comprados juntos e construir um sistema de recomendação de produtos com base no perfil dos seus clientes.

## 3. Solução do problema
- O projeto começa a partir da Análise Exploratória de Dados (EDA), etapa crucial para descobrir padrões ocultos em compras, como comportamento do consumidor, preferências de produtos, tamanho da cesta e preços médios ao longo do tempo.

- A EDA abre caminho para as *regras de associação* usadas em uma **Análise de Cesta de Mercado** com a biblioteca `apriori` em Python. Mais do que apenas usar a biblioteca, termos-chave como **antecedentes**, **consequentes**, **suporte**, **confiança** e **lift** também são explicados.

- Além disso, é desenvolvido um **sistema de recomendação** baseado na semelhança entre clientes para gerar recomendações de produtos. Assim, à medida que os clientes navegam pelo site, sua experiência é personalizada para prever o que *"eles também podem gostar"* e maximizar as vendas para a empresa.

## 4. Principais insights

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

# 5. Resultados

## Market Basket Analysis 

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

### Lendo os Resultados

- ***Antecedents:*** Estes são os itens que constituem o ponto de partida para a análise. Em outras palavras, eles estão presentes na cesta antes que o item consequente seja comprado.
- ***Consequents:*** Esses são os itens que são prováveis de serem comprados após os antecedentes.
    - Regra de associação: Se os *antecedentes* estiverem presentes na cesta, é provável que o *consequente* seja comprado.
- ***Support:*** O suporte mede com que frequência os itens de uma regra (tanto antecedentes quanto consequentes) aparecem juntos no conjunto de dados. É a proporção de transações em que os itens são comprados juntos.
- ***Confidence:*** Esta é uma medida da probabilidade de o item consequente ser comprado quando o item antecedente já está na cesta.
- ***Lift:*** O lift mede o grau de associação entre os itens antecedentes e consequentes, levando em consideração a probabilidade de compra padrão do item consequente. Um valor de lift maior que 1 indica uma associação positiva, o que significa que os itens têm mais probabilidade de serem comprados juntos do que independentemente.


## Recommendation System 
**1.** Construir uma matriz de utilidade
- A matriz de utilidade é uma matriz que contém o número de vezes que um item foi comprado (`quantity`) por cada cliente
**2.** Calcular a similaridade entre os clientes usando *cosine similarity*
- A similaridade de cosseno é uma métrica que mede a similaridade entre dois vetores
**3.** Criar um dataframe que contenha a matriz de similaridade
- Clientes como linhas e colunas com seus valores de similaridade na matriz
**4.** Gerar recomendações para cada cliente
- O objetivo é recomendar dois produtos com base nos seus três clientes mais similares
- Obter os *k* clientes mais similares
- Obter os produtos comprados pelos clientes semelhantes
- Queremos apenas os produtos que não foram comprados
- Recomendar os principais *n* produtos que não foram comprados
**5.** Criar um dataframe com as recomendações para cada cliente

## Resultados do Recommendation System 

<div align="center">

| Cliente | Produto 1                          | Produto 2                                    |
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

## 6. Conclusões
- Com os resultados gerados pela **Análise de Cesta de Mercado** e pelo **Sistema de Recomendação**, a empresa Rex London está munida com as informações necessárias para aprimorar a experiência de seus clientes e impulsionar as vendas de seus produtos.

## 7. Próximos passos
- Construção de um Dashboard interativo
  - **Análise de Cesta de Mercado:**
    - *input:* produto antecedente
    - *output:* produto consequente
  - **Sistema de Recomendação:**
    - *input:* cliente
    - *output:* dois produtos que o cliente ainda não comprou e pode comprar
