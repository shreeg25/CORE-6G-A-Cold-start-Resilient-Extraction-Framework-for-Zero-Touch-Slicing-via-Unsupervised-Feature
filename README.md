# CORE-6G: Cold-Start Resilient 6G Network Slicing Framework

![GitHub language_counts](https://img.shields.io/github/languages/count/shreeg25/CORE-6G-A-Cold-start-Resilient-Extraction-Framework-for-Zero-Touch-Slicing-via-Unsupervised-Feature)
![GitHub top language](https://img.shields.io/github/languages/top/shreeg25/CORE-6G-A-Cold-start-Resilient-Extraction-Framework-for-Zero-Touch-Slicing-via-Unsupervised-Feature)
![GitHub last commit](https://img.shields.io/github/last-commit/shreeg25/CORE-6G-A-Cold-start-Resilient-Extraction-Framework-for-Zero-Touch-Slicing-via-Unsupervised-Feature)

This project tackles the critical "cold-start problem" in 6G Zero-Touch Service Management by presenting a rigorous comparative analysis of unsupervised Gaussian Mixture Models (GMM) and supervised learning approaches (SVC, Random Forest) for autonomous network slice assignment (eMBB, uRLLC, mMTC). It demonstrates GMM's near-optimal accuracy and significant speedup, advocating for a hybrid lifecycle strategy where GMM enables Day-0 initialization before transitioning to supervised models.

## ✨ Features

- **Unsupervised GMM Classification:** Autonomous 6G network slice assignment without pre-labeled data, ideal for Day-0 operations.
- **Supervised SVC Classification:** Provides a robust baseline for comparison against unsupervised methods, using Support Vector Machines.
- **Supervised Random Forest Classification:** Another robust supervised model for comparative analysis against GMM, leveraging ensemble learning.
- **Physics-Informed Feature Engineering:** Calculates `Burstiness`, `Latency`, and `Loss` metrics from raw network flow data (`Rate`, `Size`, `Jitter`, `Duration`).
- **Real-time Data Streaming Simulation:** Simulates the ingestion of network traffic data for live processing and visualization.
- **Interactive Web Dashboard:** Flask-based web interface for uploading data, initiating simulations, and viewing classification results, performance metrics, and visualizations.
- **Dynamic Metric Display:** Real-time updates on throughput, latency, loss, accuracy, F1-score, and model-specific metrics (e.g., GMM convergence iterations, SVC support vectors, RF feature importance).
- **Automated Plot Generation:** Generates and displays confusion matrices and scatter plots of Burstiness vs. Rate for each classification model.
- **Comprehensive Result Saving:** Persists processed data, generated plots, and performance summaries to dedicated results directories.

## 🏗️ Architecture

The project employs a client-server architecture with a Flask backend processing data and machine learning models, and a web-based frontend for user interaction and visualization.

```mermaid
graph TD
    User[User/Client Browser] --> |Accesses Dashboard| Frontend("Web Frontend <br> (HTML, CSS, JS, Chart.js)")
    Frontend --> |Uploads CSVs, Triggers Ops| FlaskApp(Flask Application <br> (Python))
    FlaskApp --> |Manages ML Models| MLModels(ML Models <br> (GMM, SVC, RandomForest))
    MLModels --> |Data Preprocessing, Training, Prediction| PandasScikitLearn(Pandas & Scikit-learn)
    PandasScikitLearn --> |Generates Plots| MatplotlibSeaborn(Matplotlib & Seaborn)
    FlaskApp --> |Stores Uploads| UploadDir[CSV Uploads <br> (./uploads)]
    FlaskApp --> |Saves Results (Plots, CSVs)| ResultsDir[Results <br> (./results)]
    FlaskApp -- Git -- Github(github.com/shreeg25/CORE-6G)

    subgraph Backend
        FlaskApp
        MLModels
        PandasScikitLearn
        MatplotlibSeaborn
        UploadDir
        ResultsDir
    end
```

## 💻 Tech Stack

- **Backend:** Python 3, Flask
- **Data Manipulation:** Pandas, NumPy
- **Machine Learning:** Scikit-learn (GaussianMixture, SVC, RandomForestClassifier, StandardScaler, train_test_split, metrics)
- **Data Visualization:** Matplotlib, Seaborn, Chart.js
- **Frontend:** HTML5, CSS3, JavaScript, Bootstrap 5
- **Deployment:** Assumed local execution or containerized environment

## 📁 Project Structure

```
.
├── GMM CLassification/
│   ├── 6G_Dashboard/
│   │   ├── app.py                     # Flask application for GMM model
│   │   └── templates/
│   │       └── index.html             # HTML dashboard for GMM
│   ├── uploads/                       # Directory for uploaded GMM data
│   └── results/                       # Directory for GMM classification results
├── Random Forest Classification/
│   ├── 6G_Dashboard/
│   │   ├── app_rf.py                  # Flask application for Random Forest model
│   │   └── templates/
│   │       └── index_rf.html          # HTML dashboard for Random Forest
│   ├── uploads_rf/                    # Directory for uploaded RF data
│   └── results_rf/                    # Directory for RF classification results
├── SVC Classification/
│   ├── 6G_Dashboard/
│   │   ├── app_svc.py                 # Flask application for SVC model
│   │   └── templates/
│   │       └── index_svc.html         # HTML dashboard for SVC
│   ├── uploads_svc/                   # Directory for uploaded SVC data
│   └── results_svc/                   # Directory for SVC classification results
└── README.md
```

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

Ensure you have Python 3.x installed.

```bash
python --version
```

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/shreeg25/CORE-6G-A-Cold-start-Resilient-Extraction-Framework-for-Zero-Touch-Slicing-via-Unsupervised-Feature.git
    cd CORE-6G-A-Cold-start-Resilient-Extraction-Framework-for-Zero-Touch-Slicing-via-Unsupervised-Feature
    ```

2.  **Navigate to your desired classification directory and install dependencies.**
    Choose one of the following:

    **For GMM Classification:**
    ```bash
    cd "GMM CLassification/6G_Dashboard"
    pip install -r requirements.txt # (assuming a requirements.txt with flask, pandas, numpy, scikit-learn, matplotlib, seaborn)
    ```

    **For Random Forest Classification:**
    ```bash
    cd "Random Forest Classification/6G_Dashboard"
    pip install -r requirements.txt # (assuming a requirements.txt with flask, pandas, numpy, scikit-learn, matplotlib, seaborn)
    ```

    **For SVC Classification:**
    ```bash
    cd "SVC Classification/6G_Dashboard"
    pip install -r requirements.txt # (assuming a requirements.txt with flask, pandas, numpy, scikit-learn, matplotlib, seaborn)
    ```
    *Note: A `requirements.txt` file is not explicitly provided in the file tree, but the necessary packages are `Flask`, `pandas`, `numpy`, `scikit-learn`, `matplotlib`, and `seaborn`. You might need to create such a file or install them individually.*

    ```bash
    pip install Flask pandas numpy scikit-learn matplotlib seaborn
    ```

### Running the Application

After installing dependencies, run the Flask application for your chosen model:

**For GMM Classification:**
```bash
cd "GMM CLassification/6G_Dashboard"
python app.py
```

**For Random Forest Classification:**
```bash
cd "Random Forest Classification/6G_Dashboard"
python app_rf.py
```

**For SVC Classification:**
```bash
cd "SVC Classification/6G_Dashboard"
python app_svc.py
```

Once the application is running, open your web browser and navigate to `http://127.0.0.1:5000/`.

## ⚙️ Configuration / Environment Variables

The Flask applications are configured internally and generally do not require external environment variables for basic operation.

-   `UPLOAD_FOLDER`: Directory for uploaded CSV files.
    -   GMM: `GMM CLassification/6G_Dashboard/uploads`
    -   RF: `Random Forest Classification/6G_Dashboard/uploads_rf`
    -   SVC: `SVC Classification/6G_Dashboard/uploads_svc`
-   `RESULTS_FOLDER`: Directory where generated plots and summary CSVs are saved.
    -   GMM: `GMM CLassification/6G_Dashboard/results`
    -   RF: `Random Forest Classification/6G_Dashboard/results_rf`
    -   SVC: `SVC Classification/6G_Dashboard/results_svc`

These paths are set within each `app.py`/`app_*.py` file and are created if they don't exist:
```python
app.config['UPLOAD_FOLDER'] = 'uploads' # or 'uploads_rf', 'uploads_svc'
app.config['RESULTS_FOLDER'] = 'results' # or 'results_rf', 'results_svc'
os.makedirs(app.config['UPLOAD_FOLDER'], exist_ok=True)
os.makedirs(app.config['RESULTS_FOLDER'], exist_ok=True)
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.
