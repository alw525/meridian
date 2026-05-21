# Meridian

A career intelligence platform for graduate students, deployed at NYU's Graduate School of Arts and Science. Live at [gsasmeridian.com](https://gsasmeridian.com).

*This repository documents Meridian's architecture and methodology. The production codebase is private due to institutional data agreements.*

## What it does

Meridian classifies a graduate student's career trajectory pattern, surfaces the labor-market signal relevant to that pattern from real-time job postings, and produces advisor-facing recommendations with output validation against guardrails. The system replaced a manual, inconsistent advising workflow that did not scale; the result is a 30% reduction in advising cycle time and 5,000+ active users.

## Impact

- 5,000+ active users across the NYU graduate population
- 30% reduction in advising cycle time
- Trained on 75,000+ harmonized career records
- 12% improvement in advisor satisfaction scores following deployment
- Manuscript currently under peer review for the *Journal of Higher Education*

## Architecture

The system is built around three layers:

1. **Classification.** A scikit-learn Pipeline using TF-IDF vectorization feeds an ensemble of XGBoost, Random Forest, Logistic Regression, SVC, and Naive Bayes classifiers with dynamic ensemble weighting at inference time.

2. **Signal augmentation.** TextBlob and VADER sentiment scoring on open-text inputs, with a custom sarcasm-aware lexicon to address known sentiment-tool failure modes. Real-time labor market signal pulled from the Adzuna API.

3. **Advisor-facing output.** GPT-4 integration with prompt engineering, output validation against rule-based guardrails, and LLM monitoring for drift and degradation. A lightweight Q-table tracks correction signal from advisors for continuous improvement.

## Methodology

A worked example of one component, the sarcasm-aware sentiment ensemble, is documented in [`sentiment_ensemble_methodology.ipynb`](sentiment_ensemble_methodology.ipynb). It walks through the preprocessing, cue-based sarcasm detection, and dynamic ensemble logic on synthetic data, and includes a candid account of where the method's precision-over-recall tradeoff falls.

## Tech stack

Python, scikit-learn, XGBoost, TextBlob, VADER, OpenAI GPT-4 API, Adzuna API, Streamlit, pandas. Deployed and serving 5,000+ users at [gsasmeridian.com](https://gsasmeridian.com).

## Research foundation

Meridian is the production system that grew out of dissertation methodology research on PhD career trajectory classification. The dissertation work (cluster analysis, SHAP-based explainability for advisor trust, behavioral persona development across 75,000+ longitudinal records) defines the conceptual underpinnings; Meridian is the deployed implementation that takes that research into production at scale.

## Citation

Williams, A. (2026). *Designing PhD Career Personas Using Cluster Analysis.* Manuscript under review.

## Contact

Abby Williams, PhD
abbylwms@outlook.com
[linkedin.com/in/abbywms](https://linkedin.com/in/abbywms)

---

*Meridian was developed at NYU's Graduate School of Arts and Science (2024-2026). All intellectual property is held by NYU.*
