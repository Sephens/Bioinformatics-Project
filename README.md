# Bioinformatics Project
## Analyzing Human Preproinsulin Sequence, Calculating Molecular Weight, and Net Charge
---

This project involves the analysis of the human preproinsulin sequence, its breakdown into functional components (A-chain, B-chain, and C-peptide), and the calculation of its molecular weight using amino acid weights. Additionally, it calculates the net charge of insulin at different pH levels, providing a comprehensive example of sequence analysis and biochemical calculations in bioinformatics.

---

## **Table of Contents**
- [Bioinformatics Project](#bioinformatics-project)
  - [Analyzing Human Preproinsulin Sequence, Calculating Molecular Weight, and Net Charge](#analyzing-human-preproinsulin-sequence-calculating-molecular-weight-and-net-charge)
  - [**Table of Contents**](#table-of-contents)
  - [**1. Introduction**](#1-introduction)
  - [**2. Storing the Human Preproinsulin Sequence**](#2-storing-the-human-preproinsulin-sequence)
  - [**3. Breaking Down the Preproinsulin Sequence**](#3-breaking-down-the-preproinsulin-sequence)
  - [**4. Merging Insulin Chains**](#4-merging-insulin-chains)
  - [**5. Calculating the Molecular Weight of Insulin**](#5-calculating-the-molecular-weight-of-insulin)
    - [**5.1 Amino Acid Weights**](#51-amino-acid-weights)
    - [**5.2 Counting Amino Acids**](#52-counting-amino-acids)
    - [**5.3 Calculating Molecular Weight**](#53-calculating-molecular-weight)
  - [**6. Calculating the Net Charge of Insulin**](#6-calculating-the-net-charge-of-insulin)
    - [**6.1 pKR Values of Amino Acids**](#61-pkr-values-of-amino-acids)
    - [**6.2 Counting Relevant Amino Acids**](#62-counting-relevant-amino-acids)
    - [**6.3 Net Charge Calculation**](#63-net-charge-calculation)
  - [**7. Conclusion**](#7-conclusion)
    - [**Key Takeaways:**](#key-takeaways)

---

## **1. Introduction**

This project demonstrates the process of analyzing the human preproinsulin sequence, breaking it down into its constituent parts, calculating its molecular weight, and determining its net charge at various pH levels. These calculations are essential for understanding the biochemical properties of insulin, a critical hormone in human metabolism.

---

## **2. Storing the Human Preproinsulin Sequence**

The human preproinsulin sequence is stored in a variable called `preproInsulin`. This sequence includes the signal peptide and the insulin chains.

```python
preproInsulin = "malwmrllpllallalwgpdpaaafvnqhlcgshlvealylvcgergffytpktrreaedlqvgqvelgggpgagslqplalegslqkrgiveqcctsicslyqlenycn"
```

---

## **3. Breaking Down the Preproinsulin Sequence**

The preproinsulin sequence is broken down into smaller components:

- **lsInsulin**: The signal peptide.
- **bInsulin**: The B-chain of insulin.
- **aInsulin**: The A-chain of insulin.
- **cInsulin**: The C-peptide.

```python
lsInsulin = "malwmrllpllallalwgpdpaaa"
bInsulin = "fvnqhlcgshlvealylvcgergffytpkt"
aInsulin = "giveqcctsicslyqlenycn"
cInsulin = "rreaedlqvgqvelgggpgagslqplalegslqkr"
```

---

## **4. Merging Insulin Chains**

The B-chain and A-chain of insulin are merged into a single variable called `insulin`.

```python
insulin = bInsulin + aInsulin
```

---

## **5. Calculating the Molecular Weight of Insulin**

The molecular weight of insulin is calculated using the amino acid weights and their counts in the insulin sequence.

### **5.1 Amino Acid Weights**

A dictionary of amino acid weights is created.

```python
aaWeights = {
    'A': 89.09, 'C': 121.16, 'D': 133.10, 'E': 147.13, 'F': 165.19,
    'G': 75.07, 'H': 155.16, 'I': 131.17, 'K': 146.19, 'L': 131.17,
    'M': 149.21, 'N': 132.12, 'P': 115.13, 'Q': 146.15, 'R': 174.20,
    'S': 105.09, 'T': 119.12, 'V': 117.15, 'W': 204.23, 'Y': 181.19
}
```

### **5.2 Counting Amino Acids**

The count of each amino acid in the insulin sequence is calculated.

```python
aaCountInsulin = {
    x: float(insulin.upper().count(x)) for x in [
        'A', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 
        'P', 'Q', 'R', 'S', 'T', 'V', 'W', 'Y'
    ]
}
```

### **5.3 Calculating Molecular Weight**

The molecular weight is calculated by multiplying the count of each amino acid by its weight and summing the results.

```python
molecularWeightInsulin = sum({
    x: (aaCountInsulin[x] * aaWeights[x]) for x in [
        'A', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 
        'P', 'Q', 'R', 'S', 'T', 'V', 'W', 'Y'
    ]
}.values())
```

---

## **6. Calculating the Net Charge of Insulin**

The net charge of insulin is calculated at different pH levels using the pKR values of specific amino acids.

### **6.1 pKR Values of Amino Acids**

The pKR values for amino acids that contribute to the net charge are stored in a dictionary.

```python
pKR = {
    'y': 10.07,  # Tyrosine
    'c': 8.18,   # Cysteine
    'k': 10.53,  # Lysine
    'h': 6.00,   # Histidine
    'r': 12.48,  # Arginine
    'd': 3.65,   # Aspartic Acid
    'e': 4.25    # Glutamic Acid
}
```

### **6.2 Counting Relevant Amino Acids**

The count of each relevant amino acid in the insulin sequence is calculated.

```python
seqCount = {
    x: float(insulin.count(x)) for x in ['y', 'c', 'k', 'h', 'r', 'd', 'e']
}
```

### **6.3 Net Charge Calculation**

The net charge is calculated for pH values ranging from 0 to 14.

```python
pH = 0
while pH <= 14:
    netCharge = (
        +(sum({
            x: ((seqCount[x] * (10**pKR[x])) / ((10**pH) + (10**pKR[x])) \
            for x in ['k', 'h', 'r']
        }.values()))
        -(sum({
            x: ((seqCount[x] * (10**pH)) / ((10**pH) + (10**pKR[x])) \
            for x in ['y', 'c', 'd', 'e']
        }.values()))
    )
    print('{0:.2f}'.format(pH), netCharge)
    pH += 1
```

---

## **7. Conclusion**

This project provides a detailed analysis of the human preproinsulin sequence, including its breakdown into functional components, calculation of molecular weight, and determination of net charge at various pH levels. These calculations are essential for understanding the biochemical properties of insulin and its behavior under different physiological conditions.

---

### **Key Takeaways:**
- The preproinsulin sequence is processed to extract the A-chain, B-chain, and C-peptide.
- The molecular weight of insulin is calculated using amino acid weights and their counts.
- The net charge of insulin is calculated at different pH levels using pKR values of specific amino acids.
- This project serves as a foundational example of sequence analysis and biochemical calculations in bioinformatics.

---

This detailed markdown file provides a comprehensive explanation of the project, making it easy to understand and replicate.