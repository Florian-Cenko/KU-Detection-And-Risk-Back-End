# KU-Detection-And-Risk-Back-End

## Fork-based Version with Code Enhancements

This repository is based on the initial version of the **KU-Detection-Back-End**, originally developed by the research team of Prof. Apostolos Ampatzoglou. During my undergraduate thesis, I significantly extended and modified the tool.

While the setup and deployment instructions remain the same, this version includes **code-level improvements**, particularly in the logic responsible for **selecting commits for analysis**. These changes aim to improve performance, accuracy, or flexibility when analyzing code history.

> ℹ️ The project is otherwise based on the original architecture and retains full compatibility with the original database and API structure.

## Description

This project implements the backend API for an application designed to detect "Knowledge Units" (KU). It is built with Flask (Python) and provides endpoints for:

*   Managing a list of Git repositories (Add, List, Edit, Delete).
*   Fetching and storing commit information from repositories.
*   Performing analysis on code files from specific commits using a pre-trained CodeBERT model.
*   Monitoring the status and progress of the analysis process.
*   Retrieving the analysis results (detected KUs).

The backend interacts with a PostgreSQL database for data persistence and uses Git commands for cloning/updating repositories.

## Getting Started Guide

Follow the steps below to set up the backend locally on your machine.

### Prerequisites

*   **Git:** Installed on your system. ([Download Git](https://git-scm.com/downloads))
*   **Python:** Version 3.8 or newer is recommended. ([Download Python](https://www.python.org/downloads/)) Ensure `pip` is available.
*   **PostgreSQL:** An active PostgreSQL server installation. You will need the connection details (host, port, database name, user, password). ([Download PostgreSQL](https://www.postgresql.org/download/))

### Contribution Steps

1.  **Fork the Repository:**
    *   Click the "Fork" button in the top-right corner to create a copy in your own GitHub account.

2.  **Clone Your Fork:**
    *   Open a terminal or command prompt.
    *   Clone *your* fork locally, replacing `<your-username>`:
        ```bash
        git clone https://github.com/<your-username>/KU-Detection-And-Risk-Back-End.git
        ```
        *(Note: The repository name in your fork might be `KU-Detection-And-Risk-Back-End` if you didn't change it during the fork. Adjust the command accordingly.)*

3.  **Navigate to the Project Directory:**
    ```bash
    cd KU-Detection-And-Risk-Back-End, depending on the folder name
    ```

4.  **Create and Activate a Virtual Environment (Recommended):**
    *   Create a virtual environment:
        ```bash
        python -m venv venv
        ```
    *   Activate it:
        *   **Linux/macOS:** `source venv/bin/activate`
        *   **Windows:** `venv\Scripts\activate`

5.  **Install Dependencies:**
    *   Make sure the virtual environment is activated.
    *   Run the following command to install all necessary libraries:
        ```bash
        pip install -r requirements.txt
        ```

6.  **Database & Environment Setup:**
    *   Create a database in your PostgreSQL installation if one doesn't already exist.
    *   Change in folder api the file data_db.py 
        ```dotenv
        DB_HOST=localhost          # or your DB server address
        DB_PORT=5432               # or your DB server port
        DB_NAME=your_db_name       # Your database name
        DB_USER=your_db_user       # Your database user
        DB_PASSWORD=your_db_password # Your user's password
        CLONED_REPO_BASE_PATH=/path/to/store/cloned/repos # Directory to store cloned repos
        CODEBERT_BASE_PATH=/path/to/your/codebert/model   # Directory containing CodeBERT model files
        ```
    *   The application will attempt to create the necessary tables (`repositories`, `commits`, `analysis_results`) on first startup, but the database and user must already exist.

7.  **Configure Git Longpaths (If Required):**
    *   The application attempts to enable Git long path support (`core.longpaths = true`) on startup. This might require administrator/sudo privileges the first time.
    *   Alternatively, you can configure it manually (as administrator/sudo):
        ```bash
        git config --system core.longpaths true
        ```

8. **CodeBERT Model:**
    *   The CodeBERT model files used for analysis. You need to place these in a directory on your system.
    *   You have to download the model from [here](https://huggingface.co/nnikolaidis/java-ku/tree/main). And add it in models/codebert

## Running the Application

### Localy

1.  **Set the Flask Application:**
    *   In the terminal (with the virtual environment activated):
        *   **Linux/macOS:** `export FLASK_APP=api:create_app`
        *   **Windows:** `set FLASK_APP=api:create_app`
        *   *(Note: `api:create_app` refers to the `create_app` function within `api/__init__.py`)*

2.  **Start the Development Server:**
    ```bash
    flask run
    ```

3.  The application will typically be accessible at `http://127.0.0.1:5000`. You can view the list of available endpoints via the Swagger UI at `http://127.0.0.1:5000/swagger`.

### With Docker

...

## Technologies

*   Python
*   Flask
*   Psycopg2 (PostgreSQL Adapter)
*   Transformers (Hugging Face)
*   PyTorch / TensorFlow (Depending on the model)
*   GitPython
*   python-dotenv
*   Flask-CORS
*   Flask-Swagger-UI
