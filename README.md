# COVID-19 Prediction Model | Machine Learning Pandemic Forecasting

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/KuchikiRenji/covid19-prediction-model/blob/main/LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-KuchikiRenji-covid19--prediction--model)](https://github.com/KuchikiRenji/covid19-prediction-model)

**Predict COVID-19 spread and new cases using machine learning, historical case data, and mobility data.** This open-source project provides data pipelines, feature engineering, model training (e.g. linear regression), and interpretable forecasts to support public health planning and pandemic response.

---

## Table of Contents

- [About This Project](#about-this-project)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation & Setup](#installation--setup)
- [Usage & Scripts](#usage--scripts)
- [Project Structure](#project-structure)
- [Screenshots](#screenshots)
- [License](#license)
- [Contact & Author](#contact--author)

---

## About This Project

The **COVID-19 Prediction Model** is a data science and machine learning project that:

- **Predicts COVID-19 cases** using historical case data and mobility indicators
- **Fetches and processes** data from Our World in Data and Google Mobility Reports
- **Trains and evaluates** models (e.g. linear regression) for new-case forecasting
- **Supports country-level analysis** (e.g. Vietnam) with configurable pipelines

Use cases include pandemic trend analysis, outbreak forecasting, and supporting policymakers and researchers with reproducible, open-source tools.

---

## Features

- **Data ingestion**: Fetch COVID-19 and mobility data from multiple public sources
- **Data processing**: Clean, integrate, and migrate data with Python and C++ (SQLite)
- **Feature engineering**: Date-based, lag, and rolling-average features for better predictions
- **Model training & evaluation**: Train and evaluate ML models for new-case prediction
- **Visualization**: EDA, correlation analysis, actual vs. predicted plots, and Jupyter notebooks for interpretation
- **Country support**: User-defined country extraction and analysis

---

## Technologies Used

| Category        | Technologies |
|----------------|--------------|
| **Languages**  | Python, C++ (C++17) |
| **Data & ML**  | Pandas, NumPy, Scikit-learn, SQLite |
| **Visualization** | Matplotlib, Seaborn |
| **Build & Test** | CMake, Google Test |
| **Tools**      | Jupyter Notebook, Dill (serialization) |

<p align="left">
    <a href="https://www.python.org/downloads" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/></a>
    <a href="https://isocpp.org/" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" alt="cplusplus" width="40" height="40"/></a>
    <a href="https://www.sqlite.org/" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/9/97/Sqlite-square-icon.svg" alt="sqlite" width="40" height="40"/></a>
    <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer"><img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*uyUj__HJekKIkx58kMxlcA.png" alt="pandas" width="40" height="40"/></a>
    <a href="https://scikit-learn.org/stable/" target="_blank" rel="noreferrer"><img src="https://avatars.githubusercontent.com/u/17349883?s=200&v=4" alt="scikit-learn" width="40" height="40"/></a>
    <a href="https://matplotlib.org/" target="_blank" rel="noreferrer"><img src="https://cdn.phidgets.com/education/wp-content/uploads/2021/04/Matplotlib_icon.png" alt="matplotlib" width="40" height="40"/></a>
    <a href="https://seaborn.pydata.org/" target="_blank" rel="noreferrer"><img src="https://cdn.worldvectorlogo.com/logos/seaborn-1.svg" alt="seaborn" width="40" height="40"/></a>
    <a href="https://cmake.org/" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/1/13/Cmake.svg" alt="cmake" width="40" height="40"/></a>
    <a href="https://jupyter.org/" target="_blank" rel="noreferrer"><img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" alt="jupyter-notebook" width="40" height="40"/></a>
</p>

---

## Installation & Setup

### Prerequisites

- **Git** – for cloning the repository  
- **CMake** (3.10+) – for building the C++ components  
- **Python 3** – for data and ML scripts  
- **SQLite** – for database support  

### 1. Clone the repository

```bash
git clone https://github.com/KuchikiRenji/covid19-prediction-model.git
cd covid19-prediction-model
```

### 2. Add SQLiteCpp (C++ build)

From the project root:

```bash
git clone https://github.com/SRombauts/SQLiteCpp.git
```

Optional: turn off the linter option in `SQLiteCpp/CMakeLists.txt` (around line 388):

- Change `option(SQLITECPP_RUN_CPPLINT ... ON)` to `OFF` if the build fails due to cpplint.

### 3. Build the C++ application

```bash
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

On Windows, run the executable from the `Release` folder (e.g. `Covid19_Prediction.exe`). On Linux/macOS, the binary is typically in the `build` directory.

### 4. Python environment

```bash
pip install pandas numpy scikit-learn matplotlib seaborn dill joblib notebook
```

*(Use a virtual environment when possible.)*

---

## Usage & Scripts

Run from the **project root** (paths in scripts assume this).

| Step | Command | Description |
|------|--------|-------------|
| 1 | `python scripts/fetch_data.py` | Download COVID-19 and mobility data (may take 10–20 minutes) |
| 2 | `python scripts/migrate_data.py` | Migrate data for a chosen country to processed CSVs |
| 3 | (Optional) Run C++ app from `build` / `build/Release` | Use the built executable for C++ data processing |
| 4 | `python scripts/data_processing.py` | Process COVID-19 and mobility data for a country |
| 5 | `python scripts/eda_visualization.py` | Exploratory data analysis and visualizations |
| 6 | `python scripts/feature_engineering.py` | Build features for modeling |
| 7 | `python scripts/split_data.py` | Split data into train/test sets |
| 8 | `python scripts/model_training.py` | Train the prediction model |
| 9 | `python scripts/model_evaluation.py` | Evaluate model performance |
| 10 | Open `notebooks/interpret_predictions.ipynb` in Jupyter | Interpret and visualize predictions |

---

## Project Structure

```
covid19-prediction-model/
├── include/          # C++ headers
├── src/              # C++ source (main, data processor)
├── scripts/          # Python: fetch, migrate, process, EDA, train, evaluate
├── notebooks/        # Jupyter: interpret_predictions
├── models/           # Saved models (e.g. by country)
├── CMakeLists.txt
└── README.md
```

---

## Screenshots

| Correlation heatmap | New cases & deaths over time | Distribution of new cases |
|--------------------|------------------------------|----------------------------|
| ![Correlation heatmap](https://github.com/datpham0412/Covid19_Prediction_Model/assets/100574389/0f403266-8b3d-4c3c-ab27-28e8f5963ce1) | ![New cases and deaths over time](https://github.com/datpham0412/Covid19_Prediction_Model/assets/100574389/a51787f3-ef7f-4366-8849-ec641186a30e) | ![Distribution of new cases](https://github.com/datpham0412/Covid19_Prediction_Model/assets/100574389/59cddbbc-ca2c-4050-9b85-bd045380cac9) |

| Correlation scatter | Jupyter interpretation |
|---------------------|------------------------|
| ![Correlation scatter](https://github.com/datpham0412/Covid19_Prediction_Model/assets/100574389/3f1631c3-b8dc-4c8e-8732-92c6166ac63c) | ![Jupyter notebook](https://github.com/datpham0412/Covid19_Prediction_Model/assets/100574389/da923b42-92c2-493f-84c4-c6d08ffae03d) |

*(Screenshot URLs can be updated to your own repo assets when you host them.)*

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## Contact & Author

**KuchikiRenji**

- **GitHub:** [github.com/KuchikiRenji](https://github.com/KuchikiRenji)
- **Email:** [KuchikiRenji@outlook.com](mailto:KuchikiRenji@outlook.com)
- **Discord:** `kuchiki_renji`

For questions, collaboration, or feedback about this COVID-19 prediction model, reach out via the links above.

---

*COVID-19 prediction model · pandemic forecasting · machine learning · KuchikiRenji*
