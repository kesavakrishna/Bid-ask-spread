# CLAUDE.md - AI Assistant Guide for Bid-Ask Spread Repository

This file provides guidance for AI assistants working with this codebase.

## Project Overview

This is a **bibliometric analysis** research project studying academic literature on **bid-ask spreads** in financial markets. The codebase consists of Jupyter notebooks that analyze Scopus-exported academic paper metadata.

**Domain**: Financial research / Bibliometrics / Systematic Literature Review (SLR)

## Repository Structure

```
Bid-ask-spread/
├── README.md                    # Basic repo info
├── DOCUMENTATION.md             # Detailed documentation
├── CLAUDE.md                    # This file - AI assistant guide
└── Bibliometric Analysis/
    ├── jrfm-15-00451-v3.pdf    # Reference methodology paper
    ├── Dataset/
    │   ├── scopus 112_bidask.csv   # Primary dataset (112 papers)
    │   └── scopus 21bid_ask.csv    # Secondary dataset (21 papers)
    └── code/
        ├── slr_main.ipynb           # Main SLR - author listing
        ├── citation.ipynb           # Citation analysis
        ├── co_word_analysis.ipynb   # Keyword co-occurrence
        ├── co_authorship.ipynb      # Collaboration networks
        ├── co_citation.ipynb        # Co-citation analysis
        ├── Bibliographic_Coupling.ipynb  # Coupling analysis
        ├── coupling.ipynb           # Alternative coupling
        ├── Untitled0.ipynb          # Citation visualization
        ├── Untitled3.ipynb          # Author publication counts
        └── untitled4.ipynb          # Descriptive statistics
```

## Key Conventions

### File Naming
- Datasets use spaces in filenames: `scopus 112_bidask.csv`
- When referencing in code, use quotes: `'/content/scopus 112_bidask.csv'`
- Notebooks have inconsistent naming (some `Untitled`, some descriptive)

### Data Loading Pattern
All notebooks follow this pattern to load and combine datasets:
```python
import pandas as pd
df1 = pd.read_csv('/content/scopus 112_bidask.csv')
df2 = pd.read_csv('/content/scopus 21bid_ask.csv')
df = pd.concat([df1, df2])
```

### File Paths
- **Google Colab**: `/content/` prefix
- **Google Drive**: `/content/drive/MyDrive/` prefix
- **Local**: Adjust paths accordingly

### Dataset Schema
Key columns in the Scopus CSV files:
| Column | Type | Description |
|--------|------|-------------|
| `Authors` | string | Comma-separated author names |
| `Title` | string | Paper title |
| `Year` | int | Publication year (1987-2023) |
| `Cited by` | float | Citation count (may have NaN) |
| `DOI` | string | Digital Object Identifier |
| `Abstract` | string | Paper abstract text |
| `Author Keywords` | string | Author-provided keywords |
| `References` | string | Semicolon-separated reference list |
| `Affiliations` | string | Author institutions |

## Development Workflow

### Environment
- **Primary**: Google Colab (notebooks have Colab badges)
- **Alternative**: Local Jupyter with Python 3.7+

### Dependencies
```
pandas>=1.0
numpy>=1.18
matplotlib>=3.0
networkx>=2.4
scikit-learn>=0.22
```

### Running Notebooks
1. Open in Google Colab via badge link
2. Upload CSV files to `/content/`
3. Run cells sequentially

## Common Tasks for AI Assistants

### Adding New Analysis
1. Create notebook in `Bibliometric Analysis/code/`
2. Follow data loading pattern above
3. Use descriptive filename (avoid `Untitled`)
4. Add Colab badge for easy access

### Modifying Existing Analysis
- Notebooks are independent - changes don't cascade
- Test with small data subset first
- Preserve original output cells for reference

### Data Handling
- Always check for NaN: `pd.notna(value)`
- Author names may have leading/trailing spaces - use `.strip()`
- References are semicolon-separated: `.split(';')`

## Code Patterns

### Network Analysis (co_authorship, co_citation)
```python
import networkx as nx
G = nx.Graph()
G.add_edge(node1, node2, weight=count)
print(f"Nodes: {G.number_of_nodes()}, Edges: {G.number_of_edges()}")
```

### Text Analysis (co_word_analysis)
```python
from sklearn.feature_extraction.text import CountVectorizer
vectorizer = CountVectorizer(stop_words='english')
tf_matrix = vectorizer.fit_transform(df['Abstract'].values.astype('U'))
keywords = vectorizer.get_feature_names_out()
```

### Citation Aggregation
```python
author_citations = df.groupby('Authors')['Cited by'].sum()
top_authors = author_citations.sort_values(ascending=False)
```

## Important Notes

### Data Quality Issues
- Some `Cited by` values are NaN (use `.fillna(0)` if needed)
- Duplicate papers may exist across datasets
- Author name formats vary (some use initials, some full names)

### Known Limitations
- Notebooks designed for Colab - paths need adjustment for local use
- Some notebooks reference files that may not exist (`scopus 112_new.csv`)
- No automated tests - manual verification required

### Research Context
- Papers span 1987-2023
- Most cited: Corwin & Schultz (894 citations)
- Total papers: 133 (112 + 21)
- Total unique authors: 206

## Git Workflow

- Main development on feature branches
- Commits should describe bibliometric analysis changes
- Keep notebooks' output cells for reproducibility verification

## Quick Reference

| Task | File | Key Function |
|------|------|--------------|
| List all authors | slr_main.ipynb | Extract `Authors` column |
| Find top cited | citation.ipynb | `groupby().sum()` |
| Keyword analysis | co_word_analysis.ipynb | `CountVectorizer` |
| Author networks | co_authorship.ipynb | `networkx.Graph()` |
| Year statistics | untitled4.ipynb | `df.describe()` |

## Contact & Resources

- **Reference Paper**: `jrfm-15-00451-v3.pdf` in repository
- **Draft Document**: See `Bibliometric Analysis/Readme` for Google Docs link
