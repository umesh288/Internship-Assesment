# RFQ Similarity & Clustering Analysis

This project analyzes a set of RFQs (Requests For Quotation) for steel products, comparing them based on chemical, categorical, and grade properties. The goal is to identify similar RFQs and group them into families for efficient processing or quoting.

## Workflow Overview

1. **Data Loading**
   - RFQ data is loaded from `rfq.csv`.
   - Reference chemical properties are loaded from `reference_properties.tsv`.

2. **Preprocessing**
   - Grade names are normalized to ensure consistent matching.
   - Chemical property ranges are parsed into min, max, and midpoint values.
   - RFQs are joined with reference properties using the normalized grade.

3. **Similarity Calculation**
   - Each RFQ is compared to all others (excluding itself and exact categorical matches).
   - Similarity is computed using a weighted combination of:
     - **IoU (Intersection over Union)** for chemical intervals.
     - **Jaccard similarity** for categorical features (coating, finish, form, surface type).
     - **Exact match** for grade.
   - The top 3 most similar RFQs for each RFQ are identified.

4. **Clustering into Families**
   - RFQs are grouped into families based on their top-3 similarity matches.
   - Families are formed by merging overlapping sets of RFQs.

5. **Output**
   - The top-3 matches for each RFQ are saved as a CSV (`rfq_top3_matches.csv`).
   - Families are printed with their member RFQ IDs.

## Interpretation

- **Similarity Scores:** Higher scores indicate RFQs that are more alike in chemical composition, categorical features, and grade.
- **Families:** Each family contains RFQs that are highly similar and could be processed or quoted together, improving operational efficiency.

## Usage

Run the notebook step-by-step. Adjust similarity weights or methods as needed for ablation analysis. The output CSV and printed families can be used for further business decisions or
