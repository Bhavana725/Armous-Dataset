# Armous Dataset: HTTP Traffic Classification

## Overview

This repository contains the **Armous Dataset**, a semi-synthetic dataset designed for classifying HTTP traffic into three categories: human users, traditional bots, and LLM-driven scrapers. The dataset is grounded in real-world HTTP traffic captures and engineered features extracted from baseline behavioral patterns.

## Dataset Description

### Foundation
The dataset is derived from real-world HTTP traffic captured via proxy interceptor module and stored in the `captures.json` file. The captured logs contain detailed request-response pairs including headers, timestamps, and resource types. From these baseline captures, key behavioral features were systematically extracted and engineered to construct the final dataset.

### Feature Engineering
Statistical models were developed to extract 21 engineered features from the baseline HTTP traffic captures, including:
- Header composition metrics
- User-agent entropy measures
- Inter-arrival times
- Session patterns
- Request-response characteristics

### Dataset Generation
Using the statistical models derived from real-world captures, a semi-synthetic dataset of 5,000 instances was generated with controlled stochastic perturbations and limited label noise to reflect real-world behavioral overlap and improve model generalization.

## Dataset Composition

| Aspect | Details |
|--------|---------|
| **Total Instances** | 5,000 |
| **Total Features** | 22 (21 engineered features + 1 class label) |
| **Class Distribution** | Human (2,725), Bot (1,520), LLM-based (755) |
| **Format** | CSV |

### Class Labels
- **Label 0**: Human users (54.5%)
- **Label 1**: Traditional bots (30.4%)
- **Label 2**: LLM-driven scrapers (15.1%)

## Files

- **`armous_Dataset.csv`**: The final processed dataset containing 5,000 instances with 22 attributes
- **`captures.json`**: The baseline real-world HTTP traffic captures used as the foundation for feature extraction and dataset generation

## Privacy & Ethical Considerations

All captured data have been anonymized to preserve user privacy. Due to the potential risk of misuse in adversarial automation research, the complete dataset with identifiable metadata is not publicly released. This repository contains the anonymized, processed dataset suitable for research purposes.

For inquiries regarding access to extended dataset versions or additional documentation, please contact the authors.

## Usage

The dataset is formatted as a standard CSV file with headers. Each row represents an HTTP traffic instance with its corresponding class label.

### Loading the Dataset

```python
import pandas as pd

# Load the dataset
df = pd.read_csv('armous_Dataset.csv')

# Display basic information
print(df.info())
print(df.describe())
print(df['class_label'].value_counts())
```

### Data Exploration Example

```python
import numpy as np
import matplotlib.pyplot as plt

# Analyze class distribution
class_counts = df['class_label'].value_counts()
class_names = ['Human', 'Bot', 'LLM-based']

plt.figure(figsize=(8, 6))
plt.bar(class_names, class_counts.values)
plt.ylabel('Count')
plt.title('Armous Dataset Class Distribution')
plt.show()

# Statistical summary
print(df.describe())
```

## Dataset Features

The 21 engineered features extracted from HTTP traffic captures include metrics related to:
- **HTTP Header Patterns**: Composition and anomaly detection in request/response headers
- **User-Agent Characteristics**: Entropy measures and browser fingerprinting indicators
- **Request Timing**: Inter-arrival intervals and temporal patterns
- **Session Behavior**: User session continuity and pattern consistency
- **Resource Sequences**: Request ordering and resource type patterns
- **Protocol Indicators**: HTTP version, method distribution, and status codes

### Feature Statistics

Each feature represents a distinct aspect of HTTP traffic behavior, engineered to discriminate between:
- Legitimate human browsing patterns
- Automated traditional bot behavior
- LLM-driven web scraping patterns

*For detailed feature definitions, mathematical formulations, and comprehensive statistical distributions, refer to the accompanying research publication.*

## Methodology

### Data Collection
- Real-world HTTP traffic captured via proxy interceptor
- Sessions include complete request-response pairs with full headers
- Timestamps and resource metadata preserved for temporal analysis
- Multiple real-world sources to ensure diversity

### Feature Extraction Process
1. Parse baseline captures from `captures.json`
2. Extract behavioral features from request/response pairs
3. Compute statistical aggregates over traffic sessions
4. Normalize features for model compatibility

### Semi-Synthetic Generation
- Statistical models trained on real-world feature distributions
- Synthetic instances generated using multivariate distributions
- Controlled perturbations applied to simulate behavioral variations
- Label noise introduced to reflect real-world classification ambiguity

## Citation

If you use this dataset in your research, please cite it as follows:

```bibtex
@misc{armous_dataset_2026,
  author = {Bhavana725},
  title = {Armous Dataset: HTTP Traffic Classification Dataset},
  year = {2026},
  publisher = {GitHub},
  howpublished = {\url{https://github.com/Bhavana725/Armous-Dataset}},
  note = {Grounded in real-world HTTP traffic captures with engineered features}
}
```

### Alternative Citation Format (IEEE)

```
[X] Bhavana725, "Armous Dataset: HTTP Traffic Classification Dataset," GitHub, 2026. [Online]. Available: https://github.com/Bhavana725/Armous-Dataset. [Accessed: Mon DD, YYYY].
```

## Dataset Characteristics

### Traffic Sources
- Real-world HTTP traffic from diverse client applications
- Multiple protocol versions and client types represented
- Authentic behavioral patterns including retries and error handling

### Quality Assurance
- All personally identifiable information (PII) removed
- Malformed requests filtered and validated
- Temporal consistency verified
- Missing values handled through feature engineering

### Generalization Considerations
- Controlled stochastic perturbations ensure robustness
- Limited label noise reflects real-world classification overlap
- Feature engineering balances realism with synthetic generation
- Class imbalance reflects authentic traffic distributions

## Limitations

1. **Dataset Size**: While 5,000 instances provide a solid foundation, larger-scale collections may benefit specific applications
2. **Temporal Scope**: Captures reflect traffic patterns from a specific time period; evolving attack patterns may require updates
3. **Domain Specificity**: Traffic characteristics may vary across different target websites and protocols
4. **Anonymization Trade-off**: Privacy preservation may limit certain fine-grained feature analyses

## Ethical Use

This dataset is provided for legitimate cybersecurity research and defensive purposes. Prohibited uses include:
- Development of evasion techniques to bypass security defenses
- Unauthorized automation or web scraping
- Misuse in denial-of-service attacks or malicious automation
- Redistribution without proper attribution

## Repository Information

- **Repository**: https://github.com/Bhavana725/Armous-Dataset
- **Repository ID**: 1196292047
- **Primary Files**:
  - `armous_Dataset.csv` - Processed dataset (1.93 MB)
  - `captures.json` - Baseline real-world HTTP traffic (12.65 MB)

## Contact & Support

For questions, issues, or feedback:
- Open an issue on the GitHub repository
- Contact the dataset authors for collaboration inquiries
- Request additional documentation or extended dataset versions through proper channels

## Acknowledgments

This dataset was developed as part of research into distinguishing human users from automated traffic in HTTP communications. We acknowledge the importance of privacy preservation and ethical considerations in cybersecurity research.

## Version History

- **v1.0** (March 2026): Initial release with 5,000 instances and 21 engineered features

---

**Last Updated**: March 30, 2026  
**License**: Research Use Only  
**Status**: Actively maintained

---

## Quick Start Guide

### Requirements
```
pandas >= 1.0
numpy >= 1.18
```

### Installation
```bash
git clone https://github.com/Bhavana725/Armous-Dataset.git
cd Armous-Dataset
```

### Load and Explore
```python
import pandas as pd

# Load dataset
dataset = pd.read_csv('armous_Dataset.csv')

# Basic exploration
print(f"Dataset shape: {dataset.shape}")
print(f"\nClass distribution:\n{dataset['class_label'].value_counts()}")
print(f"\nFeature names:\n{list(dataset.columns)}")
```

### Train a Simple Classifier
```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, confusion_matrix

# Prepare data
X = dataset.drop('class_label', axis=1)
y = dataset['class_label']

# Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train
clf = RandomForestClassifier(n_estimators=100, random_state=42)
clf.fit(X_train, y_train)

# Evaluate
y_pred = clf.predict(X_test)
print(classification_report(y_test, y_pred))
```

## References

For related work on HTTP traffic classification and bot detection, see the accompanying research publication that describes the methodology, feature engineering process, and baseline results.

## Disclaimer

This dataset is provided "as is" for research purposes. The authors make no warranties regarding the completeness or accuracy of the data. Users accept full responsibility for their use of this dataset in compliance with applicable laws and ethical guidelines.
