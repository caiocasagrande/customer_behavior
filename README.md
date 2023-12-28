# Beyond "You May Also Like": Deconstructing Consumer Choices with Data Science

This Data Science project presents a data-driven approach to understand consumer behavior and personalize product recommendations using an e-commerce dataset. It holds the potential to boost sales significantly and enhance customer experience. The project is structured around three key chapters: **Exploratory Data Analysis**, **Market Basket Analysis**, and **Recommendation System**.

- The first one, the EDA, is a crucial step for uncovering hidden patterns on purchases like consumer behavior, product preferences, basket size and average prices over time.

- The EDA paves the way for the *association rule mining approach* that is used in a **Market Basket Analysis** with the `apriori` library in Python. More than only using the library, key terms like **antecedents**, **consequents**, **support**, **confidence**, and **lift** are also explained.

- Further, a **recommendation system** based on customer similarity is developed to generate recommendations of products. Thus, as the customers browses through the site, their experience is personalized in order to predict what *"they might also like"* and to maximize the sales for the company as well.

# Exploratory Data Analysis

### How is the distribution of purchases in 2011?
![image](https://github.com/caiocasagrande/customer_behavior/blob/main/images/3_2_purchases_per_day_2011.png)
- The data is more well behaved in 2011 than in 2010, but the variations are very strong 
- There are a little bit more than 10 spikes in the purchases of 2011

### How is the relation between price and quantity? The higher the price, the lower the quantity?
![image](https://github.com/caiocasagrande/customer_behavior/blob/main/images/3_8_avg_price_vs_avg_qnt.png)
- The relation between price and quantity is inversely proportional
- The average price is higher for items with a lower quantity
- The average price is lower for items with a higher quantity
- So the higher the price, the lower the quantity

### What is the behavior of *price* and *size* of baskets per month in 2011?
![image](https://github.com/caiocasagrande/customer_behavior/blob/main/images/3_10_avg_price_avg_size_basket_per_month.png)
- The average price of baskets hits the lowest point in June, followed by July
- The highest average price of baskest are seen from September to November
- September and October are also the months with the highest average size os baskets
- **Taking also into account the number of purchases per month seen earlier, we can tell that the end of the year is the best time for the company to sell its products**

# Market Basket Analysis 

## Market Basket Analysis Results

<div align="center">
  
| antecedents                                            | consequents                    | support | confidence | lift   |
|--------------------------------------------------------|--------------------------------|---------|------------|--------|
| (GREEN REGENCY TEACUP AND SAUCER, REGENC...) | (ROSES REGENCY TEACUP AND SAUCER) | 0.019   | 0.828      | 16.296 |
| (LUNCH BAG WOODLAND, LUNCH BAG PINK POLK...) | (LUNCH BAG RED RETROSPOT)       | 0.011   | 0.826      | 9.641  |
| (STRAWBERRY CHARLOTTE BAG, CHARLOTTE BAG...) | (RED RETROSPOT CHARLOTTE BAG)    | 0.012   | 0.821      | 17.765 |
| (LUNCH BAG PINK POLKADOT, LUNCH BAG SPAC...) | (LUNCH BAG BLACK SKULL.)         | 0.010   | 0.798      | 10.523 |
| (LUNCH BAG WOODLAND, LUNCH BAG PINK POLK...) | (LUNCH BAG RED RETROSPOT)       | 0.011   | 0.797      | 9.296  |
| (JUMBO BAG VINTAGE LEAF, JUMBO BAG PINK P...)| (JUMBO BAG RED RETROSPOT)       | 0.012   | 0.796      | 7.551  |
| (LUNCH BAG WOODLAND, LUNCH BAG PINK POLK...) | (LUNCH BAG RED RETROSPOT)       | 0.011   | 0.789      | 9.203  |
| (JUMBO BAG PEARS, JUMBO BAG RED RETROSPOT)   | (JUMBO BAG APPLES)              | 0.011   | 0.788      | 16.106 |
| (JUMBO BAG SCANDINAVIAN BLUE PAISLEY, JU...) | (JUMBO BAG RED RETROSPOT)       | 0.011   | 0.785      | 7.447  |
| (GREEN REGENCY TEACUP AND SAUCER)            | (ROSES REGENCY TEACUP AND SAUCER) | 0.036   | 0.779      | 15.334 |

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
