# Prework Student Notebook - New York Health Club Survey Analysis

This repository contains a Google Colab notebook (`Prework Student.ipynb`) designed for initial data exploration and answering specific questions derived from the "New York Health Club Survey" dataset.

## Table of Contents

1.  [Overview](#overview)
2.  [Key Features](#key-features)
3.  [Technologies Used](#technologies-used)
4.  [Notebook Structure and Analysis Steps](#notebook-structure-and-analysis-steps)
5.  [Key Insights and Results](#key-insights-and-results)
6.  [How to Use/Run the Notebook](#how-to-userun-the-notebook)

---

## Overview

The `Prework Student.ipynb` notebook provides a foundational example of data analysis using Python and the `pandas` library. It focuses on loading a CSV dataset, performing basic exploratory data analysis (EDA), and then extracting specific information by filtering and aggregating the data to answer predefined questions about health club survey participants.

---

## Key Features

*   **Data Loading:** Efficiently loads data from a CSV file into a pandas DataFrame.
*   **Basic EDA:** Utilizes `describe()` and `info()` to get a quick statistical summary and check data types/missing values.
*   **Data Filtering:** Demonstrates how to filter DataFrames based on specific column values to isolate subsets of data (e.g., specific 'Type' of workers).
*   **Data Aggregation:** Performs basic aggregation operations like sum, count, and mean on filtered datasets.
*   **Question Answering:** Provides a clear structure for answering specific data-driven questions.

---

## Technologies Used

*   **Python 3.x**
*   **pandas:** For data manipulation and analysis.
*   **numpy:** (Imported, but not explicitly used in the shown calculations) For numerical operations.
*   **matplotlib.pyplot:** (Imported, but not used) For data visualization (placeholder).
*   **statsmodels.api:** (Imported, but not used) For statistical modeling (placeholder).
*   **scipy.optimize:** (Imported, but not used) For optimization algorithms (placeholder).
*   **os:** For interacting with the operating system, particularly for changing directories (note: requires careful handling for portability).

---

## Notebook Structure and Analysis Steps

The notebook is organized into several cells, each performing a distinct part of the analysis:

1.  **Cell 1: Setup and Data Loading**
    *   Imports necessary libraries (`pandas`, `numpy`, `matplotlib.pyplot`, `statsmodels.api`, `scipy.optimize`, `os`).
    *   **Crucially:** Includes a line to change the working directory and then reads the `NYHCSurvey.csv` file. **Users must update the file path to their local CSV location or ensure the CSV is accessible in their Colab environment.**

    ```python
    #Import libraries
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    import statsmodels.api as sm
    import scipy.optimize as sco
    import os
    os.chdir("C:/Users/dhanush/Downloads") # <<< THIS PATH NEEDS TO BE UPDATED
    #Read data from stored CSV file (THIS SHOULD POINT TO YOUR FILE's location & name)
    NYHC = pd.read_csv('NYHCSurvey.csv')
    ```

2.  **Cell 2: Display DataFrame**
    *   Simply displays the entire `NYHC` DataFrame, showing the first and last few rows.

    ```python
    NYHC
    ```

3.  **Cell 3: Descriptive Statistics**
    *   Generates summary statistics for numerical columns using `NYHC.describe()`.

    ```python
    NYHC.describe()
    ```

4.  **Cell 4 & 5: Data Information and Type Check**
    *   Prints a concise summary of the DataFrame, including data types and non-null values using `NYHC.info()`.
    *   A markdown cell confirms that all columns are of `int64` dtype, indicating integer values.

    ```python
    print(NYHC.info())
    ```

5.  **Cell 6 & 7: Question 1 - Fixed Schedule Workers Analysis**
    *   Filters the DataFrame to include only "Fixed Schedule Workers" (where `Type == 2`).
    *   Calculates and prints the ratio of the sum of `6am_9am` column to the count of "Type" for this group.

    ```python
    # Question - 1
    # Type - 2 - Fixed Schedule Workers
    df = NYHC[NYHC["Type"] ==2]
    print(round(df["6am_9am"].sum()/df.count()["Type"],2))
    ```

6.  **Cell 8: Question 2 - Student Count**
    *   Filters the DataFrame to include only "Students" (where `Type == 1`).
    *   Counts and prints the total number of students.

    ```python
    # Question - 2
    # Type - 1 - Students
    df_students = NYHC[NYHC["Type"] == 1]
    print(df_students.count()["Type"])
    ```

7.  **Cell 9: Question 3 - Total Professionals**
    *   Filters the DataFrame for "Flexible Schedule Workers" (where `Type == 3`).
    *   Adds the count of "Fixed Schedule Workers" (from `df`) and "Flexible Schedule Workers" to get the total number of "Professionals".

    ```python
    # Question - 3
    # Number of Professionals = Number of Fixed Schedule Workers + Number of Flexible Schedule Workers.
    df_flexible = NYHC[NYHC["Type"] == 3]
    print(df.count()["Type"] + df_flexible.count()["Type"])
    ```

8.  **Cell 10: Question 4 - Specific Willingness Percentage**
    *   Counts how many entries in the entire dataset have a `9pm_close` value equal to `90.75`.
    *   States the percentage (which is 0% based on the count).

    ```python
    # Question - 4
    # Percentage of Professionals who are willing spend 90.75 on 9pm to close
    print(NYHC[NYHC["9pm_close"] == 90.75].count()[0])
    ```

9.  **Cell 11: Question 5 - Students' Afternoon Willingness**
    *   Calculates and prints the mean of the `2pm_5pm` column for the "Students" group (`df_students`).

    ```python
    # Question - 5
    print(df_students["2pm_5pm"].mean())
    ```

---

## Key Insights and Results

Based on the analysis performed in the notebook, the following key insights were derived from the `NYHCSurvey.csv` dataset:

*   **Data Types:** All columns in the dataset are of integer type (`int64`).
*   **Question 1:** The calculated activity ratio for Fixed Schedule Workers between 6 am and 9 am is approximately **85.77**.
*   **Question 2:** There are **279** students in the dataset.
*   **Question 3:** The total number of professionals (Fixed Schedule Workers + Flexible Schedule Workers) is **670**.
*   **Question 4:** **0%** of individuals in the dataset are willing to spend exactly 90.75 on the 9 pm to close time slot.
*   **Question 5:** The average willingness of students for the 2 pm to 5 pm time slot is approximately **53.05**.

---

## How to Use/Run the Notebook

To run this notebook, you will need a Python environment with the specified libraries and the `NYHCSurvey.csv` data file.

### Prerequisites

*   Python 3.x
*   `pandas` library (install via `pip install pandas`)

### Data File

*   Ensure you have the `NYHCSurvey.csv` file available.

### Running in Google Colab

1.  **Open the Notebook:** Go to Google Colab, click `File > Upload notebook`, and select `Prework Student.ipynb`.
2.  **Upload Data (Option 1 - Direct Upload):** In the Colab environment, click the folder icon on the left sidebar (Files). Then click the "Upload to session storage" icon and upload your `NYHCSurvey.csv` file. The file path will typically be `/content/NYHCSurvey.csv`.
3.  **Mount Google Drive (Option 2 - For Persistent Storage):** If your `NYHCSurvey.csv` is in Google Drive, you can mount your Drive:
    ```python
    from google.colab import drive
    drive.mount('/content/drive')
    # Then adjust your CSV path, e.g., '/content/drive/My Drive/path/to/NYHCSurvey.csv'
    ```
4.  **Adjust File Path:** In **Cell 1**, modify the `os.chdir` line and the `pd.read_csv` line to reflect the correct path to your `NYHCSurvey.csv` file. For direct upload, simply remove `os.chdir` and change `NYHCSurvey.csv` to `'/content/NYHCSurvey.csv'`.
    ```python
    # Example for direct upload to Colab
    # import os # Keep import os if you want to use it for other purposes, but not strictly needed for this file path.
    # os.chdir("/content") # This would change to the base content directory
    NYHC = pd.read_csv('/content/NYHCSurvey.csv') # Direct path
    ```
5.  **Run Cells:** Go to `Runtime > Run all` or execute cells individually by pressing `Shift + Enter`.

### Running Locally (Jupyter Notebook/JupyterLab/VS Code)

1.  **Save Files:** Place the `Prework Student.ipynb` file and the `NYHCSurvey.csv` file in the same directory on your local machine.
2.  **Open Notebook:** Open your Jupyter environment (e.g., `jupyter notebook` from your terminal) and navigate to the directory where you saved the files. Open `Prework Student.ipynb`.
3.  **Adjust File Path:** In **Cell 1**, modify the `os.chdir` line to point to the directory where your `NYHCSurvey.csv` file is located. If the notebook and CSV are in the same directory and you launch Jupyter from that directory, you might not need `os.chdir` at all, and `pd.read_csv('NYHCSurvey.csv')` would suffice.
    ```python
    # Example for local run if CSV is in the same directory as the notebook
    import pandas as pd
    # ... other imports
    # os.chdir("C:/Users/dhanush/Downloads") # You might remove or adjust this line
    NYHC = pd.read_csv('NYHCSurvey.csv') # Assumes CSV is in the current working directory
    ```
4.  **Run Cells:** Execute cells sequentially.