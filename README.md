# frequent-itemsets-group-7

#  Frequent Itemset Mining: Closed vs Maximal in Supermarket Data

 
**Project Title**: Exploring Frequent Itemsets: Closed vs Maximal in Supermarket Data  

##  Group Members & Contributions

| Name           | Contribution                                 |
|----------------|----------------------------------------------|
| Hans           | Data simulation + item pool definition       |
| Vivian         |  One-hot encoding & transaction formatting   |
| Rosamistica    |  Frequent itemset mining with Apriori        |
| Faith          |  Closed frequent itemset detection           |
| Innocent       |  Maximal frequent itemset detection          |


##  Objective

This project simulates 3000 supermarket transactions and applies **frequent pattern mining** using the Apriori algorithm. The goal is to identify and distinguish:

-  Frequent Itemsets  
-  Closed Frequent Itemsets  
-  Maximal Frequent Itemsets  

### 1. Simulate Supermarket Transactions  
 **Contributed by Hans**

- We define a pool of 30 common supermarket items.
- Then, we randomly generate 3000 transactions.
- Each transaction contains 2–7 items randomly selected from the item pool.

```python
random.seed(42)  # For reproducibility
```

### 2. One-Hot Encoding

 Contributed by Vivian

•	Converts the transaction list into a binary (0/1) format required by mlxtend's Apriori algorithm.

•	Each column represents an item; each row represents a transaction.

•	We also save the raw transactions for transparency.

```python
te = TransactionEncoder()
te_ary = te.fit(transactions).transform(transactions)
df = pd.DataFrame(te_ary, columns=te.columns_)
```

### 3. Generate Frequent Itemsets
 Contributed by Rosamistica

•	We apply the Apriori algorithm from mlxtend.frequent_patterns with min_support = 0.05 (5%).

•	The top 10 most frequent itemsets are displayed.

•	All frequent itemsets are saved in frequent_itemsets.csv.

```python
frequent_itemsets = apriori(df, min_support=0.05, use_colnames=True)
```
### 4. Identify Closed Frequent Itemsets
 Contributed by Faith

•	A closed itemset is one that has no superset with the same support.

•	We check this by comparing each itemset to all others.

•	Closed itemsets are saved in closed_itemsets.csv.

```python
def is_closed(itemset, support):
    for _, row in frequent_itemsets.iterrows():
        if itemset < row['itemsets'] and support == row['support']:
            return False
    return True
```

### 5. Identify Maximal Frequent Itemsets
 Contributed by Innocent

•	A maximal itemset has no frequent superset at all.

•	This is useful for reducing redundancy when mining rules.

•	Maximal itemsets are saved in maximal_itemsets.csv.

```python
def is_maximal(itemset):
    for _, row in frequent_itemsets.iterrows():
        if itemset < row['itemsets']:
            return False
    return True
```

### Output Files

|File Name	                  |Description
|-----------------------------|-----------------------------------------
|supermarket_transactions.csv |Raw transaction list (CSV)
|frequent_itemsets.csv	      |All frequent itemsets with support values
|closed_itemsets.csv	      |All closed frequent itemsets
|maximal_itemsets.csv	      |All maximal frequent itemsets

### Libraries Used
•	pandas for data manipulation

•	random for simulating data

•	mlxtend for frequent pattern mining

•	IPython.display for clean output (optional in Jupyter)

### How to Run the Code
1.	Clone the repository
2.	Install dependencies:
bash
CopyEdit
pip install pandas mlxtend
3.	Run the Python script or Jupyter Notebook
4.	View outputs in terminal or exported CSV files


## Conclusion
This project successfully demonstrates the generation of frequent, closed, and maximal itemsets from simulated supermarket data. The step-by-step approach also highlights how to preprocess transactional data and apply frequent pattern mining techniques using Python.

