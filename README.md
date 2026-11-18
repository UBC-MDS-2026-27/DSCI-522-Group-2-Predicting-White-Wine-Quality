
# Predicting White Wine Quality Using Physicochemical Properties

## Authors

- Ivan Tse
- Nidhi Danda
- Yunjin Zhang (Alice)
- Weizhuo Zhang (Nathan)

## Project Summary

This project investigates whether the physicochemical properties of Portuguese white wines can be used to predict their sensory quality scores. Using the White Wine Quality dataset from the UCI Machine Learning Repository, we apply regression analysis to examine the relationship between chemical measurements, such as alcohol content, acidity, and residual sugar, and wine quality. Our findings suggest that **[briefly describe your main findings after completing the analysis]**. These results may help provide insight into which chemical properties are associated with higher wine quality, although chemical measurements alone may not fully explain subjective human preferences.

## How to Run the Analysis

Follow these steps to reproduce the analysis on your local machine.

### 1. Clone the repository

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Predicting-White-Wine-Quality.git
cd DSCI-522-Predicting-White-Wine-Quality
```

### 2. Install dependencies

This project uses Python and `uv` to manage its dependencies.

Install `uv` if you do not already have it:

```bash
pip install uv
```

Install the project dependencies:

```bash
uv sync
```

### 3. Install Quarto

Download and install Quarto from:

https://quarto.org/docs/get-started/

Verify that Quarto is installed:

```bash
quarto --version
```

### 4. Render the report

Render the Quarto document using:

```bash
uv run quarto render white-wine-quality.qmd
```

Make sure you're in the analysis directory before running the above command. The rendered HTML report will be generated in the analysis directory.

Open `white-wine-quality.html` in your browser to view the analysis.

## Dependencies

The main dependencies and tools used in this project include:

- Python
- uv (Python package and environment manager)
- Quarto (document rendering)
- pandas (data manipulation)
- numpy (numerical operations)
- matplotlib (data visualization)
- scikit-learn (regression modelling and evaluation)

See `pyproject.toml` and `uv.lock` for the complete list of Python dependencies and their versions.

## Data Sources

The project uses the White Wine Quality dataset from the UCI Machine Learning Repository.

Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). Wine Quality. UCI Machine Learning Repository.

Dataset: https://archive.ics.uci.edu/dataset/186/wine+quality

The dataset contains 4,898 white wine samples from the Vinho Verde region of Portugal. Each observation includes 11 physicochemical measurements and a sensory quality score.

## Licenses

This project uses the following licenses:

- Project source code: [MIT License](LICENSE.md)
- Project Report: [Creative Commons Attribution 4.0 International (CC BY-NC-ND 4.0)](LICENSE.md)

See `LICENSE.md` for additional information.

## AI Use Statement

Generative AI tools were used during the development of this project.

ChatGPT was used to assist with:
- Understanding the project requirements and planning the analysis.
- Brainstorming potential research questions.
- Explaining statistical and machine learning concepts.
- Troubleshooting Python code and Quarto formatting.
- Reviewing and improving the clarity of written explanations.

All code, statistical analyses, interpretations, and final written content were reviewed and verified by the project authors.

Example prompts:
- "Help me develop a research question using the Wine Quality dataset."
- "Explain how to perform a regression analysis using scikit-learn."
- "Help me interpret the RMSE of my regression model."
- "Explain how to split data into training and testing sets without data leakage."

No additional AI instruction files were used. 

## Rendered Report

View the rendered analysis here:

[Predicting White Wine Quality Using Physicochemical Properties](Link when it's ready)
