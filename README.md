
# Predicting White Wine Quality Using Physicochemical Properties

## Authors

- Ivan Tse
- Nidhi Danda
- Yunjin Zhang (Alice)
- Weizhuo Zhang (Nathan)

## About

This project investigates whether the physicochemical properties of Portuguese white wines can be used to predict their sensory quality scores. Using the White Wine Quality dataset from the UCI Machine Learning Repository, we apply regression analysis to examine the relationship between chemical measurements, such as alcohol content, acidity, and residual sugar, and wine quality. Our findings show that a Random Forest regression model achieved a Root Mean Squared Error (RMSE) of 0.591 and a Mean Absolute Error (MAE) of 0.419 on the held-out test data. This indicates that the model's predictions differed from the observed wine quality scores by approximately 0.419 points on average. These results suggest that physicochemical measurements can provide useful information for predicting wine quality, although chemical measurements alone may not fully explain subjective human preferences.


## Report

The final report can be found here (HTML)[https://ubc-mds-2026-27.github.io/DSCI-522-Group-2-Predicting-White-Wine-Quality/].

## Usage

We run the analysis in a Docker container, so the same software and package versions are used. The image is published on Docker Hub at (link)[https://hub.docker.com/r/nathanzhang96/dsci-522-group-2-predicting-white-wine-quality]

### Setup

If it is your first time running this project, install and launch (Docker)[https://www.docker.com/get-started/], then clone this repository and move into it:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Predicting-White-Wine-Quality.git
cd DSCI-522-Predicting-White-Wine-Quality
```
Run all the commands below from the root of this repository.

### 1. Make an ssh key

If you don't have an ssh key yet, make one and press Enter at each question:

```bash
ssh-keygen -t ed25519
```

The container lets you log in with this key. If you skip this step, Docker makes a folder named ~/.ssh/id_ed25519.pub instead, and connecting to the container over ssh fails until you delete that folder and make the key.

### 2. Download the image

```bash
docker compose pull
```

### 3. Run the analysis and render the report
```bash
docker compose run --rm analysis-env uv run quarto render
```

Rendering runs the whole analysis from scratch: it downloads the data again from the UCI Machine Learning Repository (so you need an internet connection), and overwrites the files in white-wine-quality_files. The rendered report is written to analysis/white-wine-quality.html, replacing the versions in this repository. Because of --rm, the container is removed by itself when the render finishes, so there is nothing to stop afterwards.

## Contributing

Want to change the analysis, add a package, or update the published report? See [CONTRIBUTING.md](CONTRIBUTING.md).

## Dependencies

Docker

The image is built from the Dockerfile in this repository. It installs Quarto, uv, and Python with the packages listed in pyproject.toml (exact versions are locked in uv.lock).

## AI Use Statement

Generative AI tools were used during the development of this project.

ChatGPT was used to assist with:
- Understanding the project requirements and planning the analysis.
- Brainstorming potential research questions.
- Explaining statistical and machine learning concepts.
- Troubleshooting Python code and Quarto formatting and Docker containerization.
- Reviewing and improving the clarity of written explanations.

All code, statistical analyses, interpretations, and final written content were reviewed and verified by the project authors.

Example prompts:
- "Help me develop a research question using the Wine Quality dataset."
- "Explain how to perform a regression analysis using scikit-learn."
- "Help me interpret the RMSE of my regression model."
- "Explain how to split data into training and testing sets without data leakage."

No additional AI instruction files were used. 

## Licenses

This project uses the following licenses:

- Project source code: [MIT License](LICENSE.md)
- Project Report: [Creative Commons Attribution 4.0 International (CC BY-NC-ND 4.0)](LICENSE.md)

See `LICENSE.md` for additional information.


## References

Cortez, Paulo, António Cerdeira, Fernando Almeida, Telmo Matos, and José Reis. 2009. “Modeling Wine Preferences by Data Mining from Physicochemical Properties.” Decision Support Systems 47 (4): 547–53. https://doi.org/10.1016/j.dss.2009.05.016.

Natalie Harris, Claudia Gonzalez Viejo, Christopher Barnes, Alexis Pang, Sigfredo Fuentes. 2023. "Wine quality assessment for Shiraz vertical vintages based on digital technologies and machine learning modeling", Food Bioscience, Volume 56, 2023, 103354, ISSN 2212-4292. https://doi.org/10.1016/j.fbio.2023.103354.

María-Pilar Sáenz-Navajas, Chelo Ferreira, Susan E.P. Bastian, David W. Jeffery. 2025. "Bagging and boosting machine learning algorithms for modelling sensory perception from simple chemical variables: Wine mouthfeel as a case study", Food Quality and Preference, Volume 129, 2025, 105494, ISSN 0950-3293. https://doi.org/10.1016/j.foodqual.2025.105494.

Agyemang, Perpetual Opoku. 2010. “Modeling the Preference of Wine Quality Using Logistic Regression Techniques Based on Physicochemical Properties.” Master’s thesis, Youngstown State University. http://hdl.handle.net/1989/10638.

Angus, Dale. 2019. “Modeling Wine Quality from Physicochemical Properties.” CS229: Machine Learning project report, Stanford University. https://cs229.stanford.edu/proj2019aut/data/assignment_308832_raw/25895690.pdf.

