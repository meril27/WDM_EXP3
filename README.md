### EX3 Implementation of GSP Algorithm In Python
### DATE: 06.02.2026
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>

### Program:

```python
from collections import defaultdict
from itertools import combinations

# Generate candidate patterns of length k
def generate_candidates(dataset, k, min_support):
    counter = defaultdict(int)

    for seq in dataset:
        flat = []
        for itemset in seq:
            flat.extend(itemset)

        for comb in set(combinations(sorted(flat), k)):
            counter[comb] += 1

    return {p: s for p, s in counter.items() if s >= min_support}

# GSP-style algorithm
def gsp(dataset, min_support):
    k = 1
    results = {}

    while True:
        freq = generate_candidates(dataset, k, min_support)
        if not freq:
            break
        results[k] = freq
        k += 1

    return results

# Dataset 1
Dataset_1 = [
    ["a","b","c","b","e","c","f","g","a","b","e"],
    ["a","d","b","c","c","f","g","c","h"],
    ["b","c","a","d","e","b","f","c","d","f","g","h"],
    ["c","e","c","e","h"]
]


# Minimum support
min_support = 3

# Run GSP
res1 = gsp(dataset_1, min_support)


# Print results in perfect table format
def print_results(results, name):
    print(f"\n{name}")

    for k in sorted(results.keys()):
        print(f"\n{k}-Length Patterns")
        print("-" * 42)
        print("Pattern".ljust(30), "Support".rjust(6))
        print("-" * 42)

        for pattern, support in sorted(results[k].items()):
            print(str(pattern).ljust(30), str(support).rjust(4))

# Display output
print_results(res1, "Frequent Sequential Patterns - Dataset_1:")

```
### Output:

<img width="1046" height="687" alt="Screenshot 2026-02-06 153829" src="https://github.com/user-attachments/assets/d01651e9-fea9-4d29-8dfd-1218565feafe" />

<img width="1047" height="795" alt="Screenshot 2026-02-06 153856" src="https://github.com/user-attachments/assets/4cec8f58-ab21-4104-b721-beb0901ee349" />

<img width="1049" height="338" alt="Screenshot 2026-02-06 153922" src="https://github.com/user-attachments/assets/a4195da2-0401-4a5e-a04c-b8024e73b602" />


### Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(Dataset_1_result, 'Dataset_1')
```
### Output:

<img width="1332" height="746" alt="Screenshot 2026-02-06 153945" src="https://github.com/user-attachments/assets/60f302da-5f4f-45f7-813b-0d4d64cdecb7" />



### Result:
Hence, the GSP algorithm successfully identified frequent sequential patterns of lengths for the given dataset based on the specified minimum support threshold using python.
