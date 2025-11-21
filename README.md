# fram-assignment

This repository contains the code for the FIN F414 - Financial Risk Analytics & Management assignment.

## Setup

This project uses [astral uv](https://github.com/astral-sh/uv) for dependency management.

1. **Install uv**:
   If you haven't installed `uv` yet, you can do so by following the instructions in their documentation.

2. **Install Dependencies**:
   Run the following command to sync the project dependencies:

   ```bash
   uv sync
   ```

3. **Run the Project**:
   The project consists of a series of Jupyter notebooks that should be executed sequentially.

## Project Structure & Workflow

The analysis is divided into the following steps, represented by individual notebooks:

### 1. `preprocessing.ipynb`

* **Purpose**: Prepares the raw data for analysis.
* **Process**:
  * Reads the raw Excel file (`data/GR_20.xlsx`).
  * Extracts relevant datasets: Set, Ratings, Amount, LGD (Loss Given Default), and EAD (Exposure at Default).
  * Cleans and formats the data, renaming columns to "Year 1" to "Year 10".
  * Saves the processed datasets as individual CSV files in the `data/` directory for easy access in subsequent steps.

### 2. `analysis.ipynb`

* **Purpose**: Performs Exploratory Data Analysis (EDA) on the portfolio.
* **Process**:
  * Loads the processed CSV files.
  * Visualizes the evolution of the portfolio's credit quality over time.
  * Generates plots (e.g., stacked area charts) to show the distribution of credit ratings across different years.

### 3. `transition_matrix.ipynb`

* **Purpose**: Calculates the probability of credit rating migration.
* **Process**:
  * Computes the transition matrices for each year-over-year period (e.g., Year 1 to Year 2).
  * Determines the probability of a borrower moving from one rating category to another (including Default).
  * Calculates the average transition matrix to observe long-term trends.
  * Saves the yearly transition matrices to the `results/` directory.

### 4. `expected_loss.ipynb`

* **Purpose**: Estimates the Expected Loss (EL) for the portfolio.
* **Process**:
  * **Probability of Default (PD)**: Derives PDs from the calculated transition matrices (specifically the probability of transitioning to 'D').
  * **Exposure at Default (EAD)**: Calculates EAD by multiplying the loan Amount by the EAD multiplier.
  * **Expected Loss Calculation**: Computes EL using the standard formula:
    $$EL = PD \times LGD \times EAD$$
  * Saves the calculated Probability of Default and Expected Loss to `results/`.

### 5. `stress_testing.ipynb`

* **Purpose**: Evaluates the portfolio's resilience under adverse scenarios.
* **Process**:
  * **Scenario 1 (LGD Stress)**: Applies stress multipliers to the LGD values to simulate a severe economic downturn where recovery rates drop. Recalculates Expected Loss under these conditions.
  * **Scenario 2 (Rating Downgrade)**: Simulates a systemic credit quality deterioration by downgrading ratings (e.g., AAA -> A, A -> BBB). Recalculates Expected Loss based on the stressed ratings.
  * Compares the stressed Expected Loss against the baseline.
