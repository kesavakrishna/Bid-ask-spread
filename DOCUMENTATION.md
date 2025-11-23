# Bid-Ask Spread Bibliometric Analysis - Documentation

This repository contains a comprehensive bibliometric analysis of academic research on **bid-ask spreads** in financial markets. The analysis uses data exported from Scopus and implements various bibliometric techniques using Python and Jupyter notebooks.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Repository Structure](#repository-structure)
3. [Dataset Description](#dataset-description)
4. [Code Files Detailed Documentation](#code-files-detailed-documentation)
5. [Dependencies](#dependencies)
6. [How to Run](#how-to-run)

---

## Project Overview

The bid-ask spread is a fundamental concept in financial markets, representing the difference between the highest price a buyer is willing to pay (bid) and the lowest price a seller is willing to accept (ask). This repository performs bibliometric analysis on academic literature related to bid-ask spreads to understand:

- Research trends over time
- Key authors and their contributions
- Citation patterns
- Collaboration networks
- Thematic clusters through keyword analysis

The analysis covers **133 academic papers** (112 + 21 from two datasets) spanning from **1987 to 2023**.

---

## Repository Structure

```
Bid-ask-spread/
├── README.md                           # Basic repository information
├── DOCUMENTATION.md                    # This comprehensive documentation file
└── Bibliometric Analysis/
    ├── Readme                          # Reference paper and draft links
    ├── jrfm-15-00451-v3.pdf           # Reference paper on bibliometric methodology
    ├── Dataset/
    │   ├── Readme                      # Dataset information
    │   ├── scopus 112_bidask.csv       # Primary dataset (112 papers)
    │   └── scopus 21bid_ask.csv        # Secondary dataset (21 papers)
    └── code/
        ├── Readme                      # Code directory information
        ├── slr_main.ipynb              # Main SLR analysis - Author extraction
        ├── citation.ipynb              # Citation analysis
        ├── co_word_analysis.ipynb      # Keyword co-occurrence analysis
        ├── co_authorship.ipynb         # Co-authorship network analysis
        ├── co_citation.ipynb           # Co-citation analysis
        ├── Bibliographic_Coupling.ipynb # Bibliographic coupling analysis
        ├── coupling.ipynb              # Alternative coupling analysis
        ├── Untitled0.ipynb             # Citation statistics visualization
        ├── Untitled3.ipynb             # Author publication counts
        └── untitled4.ipynb             # Descriptive statistics analysis
```

---

## Dataset Description

### Source
Data is exported from **Scopus**, a major academic database, containing metadata about academic papers related to bid-ask spread research.

### Files

#### `scopus 112_bidask.csv` (Primary Dataset)
- **Records**: 112 academic papers
- **Time Range**: 1987 - 2023
- **Average Citations**: ~26 per paper

#### `scopus 21bid_ask.csv` (Secondary Dataset)
- **Records**: 21 academic papers
- **Time Range**: 1990 - 2021
- **Average Citations**: ~36 per paper

### Dataset Columns

| Column | Description |
|--------|-------------|
| `Authors` | List of paper authors |
| `Author(s) ID` | Scopus author identifiers |
| `Title` | Paper title |
| `Year` | Publication year |
| `Source title` | Journal/conference name |
| `Volume`, `Issue` | Publication volume and issue |
| `Page start`, `Page end` | Page range |
| `Cited by` | Number of citations received |
| `DOI` | Digital Object Identifier |
| `Link` | URL to the paper |
| `Affiliations` | Author institutional affiliations |
| `Abstract` | Paper abstract text |
| `Author Keywords` | Keywords provided by authors |
| `Index Keywords` | Scopus-assigned keywords |
| `References` | List of cited references |
| `Document Type` | Article, Review, etc. |
| `Language` | Publication language |

---

## Code Files Detailed Documentation

### 1. `slr_main.ipynb` - Systematic Literature Review Main Analysis

**Purpose**: Extracts and lists all author names from the combined dataset.

**What it does**:
- Loads both CSV datasets using pandas
- Concatenates them into a single DataFrame
- Extracts the `Authors` column
- Prints a complete list of all author names

**Key Output**: List of all 133 author groups from the papers

**Libraries Used**: `pandas`, `matplotlib`

---

### 2. `citation.ipynb` - Citation Analysis

**Purpose**: Analyzes citation patterns to identify the most influential papers and authors.

**What it does**:
1. **Author Citation Analysis**: Groups papers by author and sums their citations
2. **Title Citation Analysis**: Ranks papers by their citation counts
3. **DOI Citation Analysis**: Lists top DOIs by citation count
4. **Visualization**: Creates bar charts showing top 10 authors by citations

**Key Findings**:
- **Most Cited Paper**: "A Simple Way to Estimate Bid-Ask Spreads from Daily High and Low Prices" by Corwin & Schultz (894 citations)
- **Top Authors**: Corwin S.A. & Schultz P. (894), GLOSTEN L.R. (177), Bollerslev T. & Melvin M. (160)

**Libraries Used**: `pandas`, `matplotlib`

---

### 3. `co_word_analysis.ipynb` - Keyword Co-occurrence Analysis

**Purpose**: Identifies frequently co-occurring keywords in paper abstracts to reveal thematic relationships.

**What it does**:
1. Uses `CountVectorizer` from scikit-learn to tokenize abstracts
2. Removes English stop words
3. Calculates co-occurrence counts for all keyword pairs
4. Creates a network graph of keyword relationships
5. Ranks keyword pairs by co-occurrence frequency

**Key Findings** (Top Keyword Pairs):
| Keyword Pair | Co-occurrence Count |
|--------------|---------------------|
| (ask, bid) | 120 |
| (ask, spread) | 98 |
| (bid, spread) | 98 |
| (ask, data) | 72 |
| (bid, market) | 66 |
| (bid, estimation) | 65 |

**Libraries Used**: `pandas`, `sklearn.feature_extraction.text`, `networkx`, `collections.defaultdict`

---

### 4. `co_authorship.ipynb` - Co-authorship Network Analysis

**Purpose**: Maps collaboration patterns between authors through network analysis.

**What it does**:
1. Parses author names from each paper (comma-separated)
2. Creates edges between co-authors who published together
3. Builds a NetworkX graph representing collaboration network
4. Includes affiliation information as edge attributes

**Key Statistics**:
- **Number of Authors (nodes)**: 206
- **Number of Co-authorships (edges)**: 201

**Libraries Used**: `pandas`, `networkx`, `matplotlib`

---

### 5. `co_citation.ipynb` - Co-citation Analysis

**Purpose**: Identifies papers that are frequently cited together, revealing intellectual connections.

**What it does**:
1. Extracts reference lists from both datasets
2. Finds pairs of references that appear together in citing papers
3. Creates a co-citation network graph
4. Generates a co-citation matrix for visualization
5. Uses binary matrix representation (1 = co-cited, 0 = not)

**Output**:
- List of co-citation relationships
- Visual co-citation matrix heatmap

**Libraries Used**: `pandas`, `networkx`, `matplotlib`, `numpy`, `itertools`

---

### 6. `Bibliographic_Coupling.ipynb` - Bibliographic Coupling Analysis

**Purpose**: Measures similarity between papers based on shared references.

**What it does**:
1. Extracts reference lists from each paper
2. Splits references by semicolon delimiter
3. Calculates intersection of reference sets between paper pairs
4. Counts coupling strength (number of shared references)
5. Ranks paper pairs by coupling count

**Key Findings** (Top Coupled Reference Pairs):
| Reference Pair | Coupling Count |
|----------------|----------------|
| Abdi, F., Ranaldo, A. works | 70 |
| Aitken, M., Frino, A. works | 67 |
| Agarwal, P., O'Hara, M. works | 66 |
| Akerlof, G. (Market for Lemons) | 48 |
| Amihud, Y., Mendelson, H. works | 40 |

**Libraries Used**: `pandas`, `collections.defaultdict`

---

### 7. `coupling.ipynb` - Alternative Coupling Analysis

**Purpose**: Alternative implementation of bibliographic coupling using DOIs.

**What it does**:
1. Uses DOI field instead of full references
2. Splits DOIs by semicolon
3. Calculates coupling between DOI pairs
4. Simpler implementation focused on DOI-based coupling

**Libraries Used**: `pandas`, `collections.defaultdict`

---

### 8. `Untitled0.ipynb` - Citation Statistics Visualization

**Purpose**: Visualizes author citation distributions.

**What it does**:
1. Calculates total citations per author
2. Sorts authors by citation count
3. Creates bar chart of top 10 authors by citations

**Libraries Used**: `pandas`, `matplotlib`

---

### 9. `Untitled3.ipynb` - Author Publication Counts

**Purpose**: Counts publications per author to identify prolific researchers.

**What it does**:
1. Counts occurrences of each author entry
2. Creates co-authorship network (alternative method using semicolon splitting)
3. Lists authors by publication frequency

**Key Findings** (Most Prolific Authors):
| Author | Publication Count |
|--------|-------------------|
| Frank J., Garcia P. | 3 |
| Bleaney M., Li Z. | 3 |
| Theissen E. | 2 |

**Libraries Used**: `pandas`, `networkx`

---

### 10. `untitled4.ipynb` - Descriptive Statistics Analysis

**Purpose**: Provides comprehensive descriptive statistics for both datasets.

**What it does**:
1. **Extracts metadata**: Authors, Titles, Years, Keywords from both datasets
2. **Year Statistics**: Mean, std, min, max publication years
3. **Citation Statistics**: Distribution of citation counts
4. **Visualizations**:
   - Publication year distribution (bar chart)
   - Publication year vs. citation count (scatter plot)
5. **Author-Affiliation Analysis**: Splits and prepares data for network analysis

**Key Statistics**:

| Metric | Dataset 1 (112 papers) | Dataset 2 (21 papers) |
|--------|------------------------|------------------------|
| Mean Year | 2010.8 | 2011.7 |
| Std Year | 9.87 | 8.32 |
| Year Range | 1987-2023 | 1990-2021 |
| Mean Citations | 25.76 | 36.12 |
| Max Citations | 447 | 447 |

**Libraries Used**: `pandas`, `matplotlib`

---

## Dependencies

To run the notebooks, install the following Python packages:

```bash
pip install pandas numpy matplotlib networkx scikit-learn
```

### Required Libraries

| Library | Version | Purpose |
|---------|---------|---------|
| pandas | >= 1.0 | Data manipulation and CSV reading |
| numpy | >= 1.18 | Numerical operations |
| matplotlib | >= 3.0 | Data visualization |
| networkx | >= 2.4 | Network graph analysis |
| scikit-learn | >= 0.22 | Text vectorization (CountVectorizer) |

---

## How to Run

### Option 1: Google Colab (Recommended)
Each notebook includes a "Open in Colab" badge. Click the badge to run directly in Google Colab.

**Steps**:
1. Click the Colab badge in any notebook
2. Upload the CSV datasets to Colab's `/content/` directory
3. Run all cells

### Option 2: Local Jupyter Environment

```bash
# Clone the repository
git clone https://github.com/kesavakrishna/Bid-ask-spread.git
cd Bid-ask-spread

# Install dependencies
pip install pandas numpy matplotlib networkx scikit-learn

# Launch Jupyter
jupyter notebook

# Navigate to Bibliometric Analysis/code/
# Update file paths in notebooks to match local paths
```

### Important Notes
- Update CSV file paths in notebooks to match your environment
- For Google Drive access (some notebooks), mount drive first:
  ```python
  from google.colab import drive
  drive.mount('/content/drive')
  ```

---

## Reference Paper

This analysis methodology is inspired by:
- **File**: `jrfm-15-00451-v3.pdf`
- **Title**: "What Do We Know about Crowdfunding and P2P Lending Research? A Bibliometric Review and Meta-Analysis"
- **First Draft**: [Google Docs Link](https://docs.google.com/document/d/1pm4nlGCJnh37JhBvbN1ZLH8geyVdvutQFo-sq0AmcY4/edit?usp=sharing)

---

## Summary of Analyses

| Analysis Type | Notebook | Key Insight |
|---------------|----------|-------------|
| Author Listing | slr_main.ipynb | 133 papers from 206 unique authors |
| Citation Analysis | citation.ipynb | Corwin & Schultz most cited (894) |
| Keyword Co-occurrence | co_word_analysis.ipynb | "bid-ask-spread" most frequent theme |
| Co-authorship | co_authorship.ipynb | 201 collaboration links |
| Co-citation | co_citation.ipynb | Intellectual structure mapping |
| Bibliographic Coupling | Bibliographic_Coupling.ipynb | Shared reference patterns |
| Descriptive Stats | untitled4.ipynb | Research spans 1987-2023 |

---

## License

This repository is for academic research purposes.

---

*Documentation generated for the Bid-Ask Spread Bibliometric Analysis repository.*
