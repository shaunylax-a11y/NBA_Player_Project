# Project - NBA Player Statistics – Exploratory Data Analysis

## Dataset

This project uses the **NBA Player dataset** (`all_seasons.csv`).

**Source:**
https://www.kaggle.com/datasets/salikhussaini49/nba-data

The dataset contains NBA player season statistics across multiple years, including variables such as:

* points per game
* rebounds
* assists
* usage percentage
* team information
* season information

This makes it useful for exploring player performance, trends over time, and relationships between different basketball statistics.

**Note:** The raw dataset is not included in this repository and is intentionally excluded through `.gitignore`.

---

## Project Overview

This project explores NBA player statistics across multiple seasons using **Python** and **Jupyter Notebook**. The analysis focuses on understanding the structure of the dataset, summarizing important variables, creating visualizations, and strengthening the dataset by joining it with a second table containing conference and division information.

The project is not just about making graphs. It also shows how a real dataset can be inspected, interpreted, improved with a join, and organized into a cleaner GitHub project structure.

---

## Data Source

The main dataset used in this project is `all_seasons.csv`, an NBA player statistics dataset.

A second dataset, `team_lookup.csv`, was manually created to support joining and add team-level context. This second file was joined using `team_abbreviation` so that the dataset could include:

* `conference`
* `division`

This was done to make the analysis more useful by adding context that the original player dataset did not include on its own.

---

## Project Goals

The goals of this project are to:

* inspect and understand the dataset
* summarize the data
* create useful charts and descriptive analysis
* join the dataset with another related dataset
* explain insights and limitations clearly
* organize the project in a way that is easier to navigate and understand

---

## Research Questions

This project is guided by the following questions:

1. What does the distribution of points per game look like across player-season records?
2. How has average points per game changed across NBA seasons?
3. Is there a relationship between usage percentage and points per game?
4. What additional insight can be gained by joining team-level conference and division information to the player dataset?

These questions help give the notebook a clearer purpose and make the analysis more focused.

---

## Repository Structure

### Root files

* `README.md`
  Main overview of the project, dataset, goals, and folder structure.

* `LICENSE`
  License information for the repository.

* `.gitignore`
  Keeps raw data files and unnecessary system/notebook files off GitHub.

* `CITATIONS.md`
  Contains source notes and AI-use information.

* `requirements.txt`
  Lists the main Python packages needed to run the project.

---

### Folders

* `data/`
  Contains local raw data files and lookup tables used in the project.

* `clean_data/`
  Contains cleaned or joined output files, such as the merged NBA dataset with conference and division information.

* `scripts/`
  Contains Python scripts used for repeatable project tasks, such as joining datasets and generating summary tables.

* `analysis/`
  Contains the main notebook and exported HTML/Markdown versions of the analysis.

* `results/`
  Contains saved summary tables and visual outputs created from the analysis.

* `images/`
  Contains screenshots used for the reflection or project documentation.

* `docs/`
  Contains shorter supporting project documentation, such as a project summary.

---

## Main Files and What They Do

* `analysis/analysis.ipynb`
  The main notebook where the full analysis, explanations, tables, and visualizations are shown.

* `analysis/analysis.html`
  Exported HTML version of the notebook for easier viewing outside Jupyter.

* `analysis/analysis.md`
  Exported Markdown version of the notebook.

* `scripts/join_team_info.py`
  Joins the NBA dataset with the `team_lookup.csv` file using `team_abbreviation`.

* `scripts/make_summary_tables.py`
  Creates reusable summary tables and saves them into the `results/` folder.

* `clean_data/nba_players_with_team_info.csv`
  Joined dataset containing the original NBA player data plus conference and division information.

---

## Analysis Summary

The analysis includes:

* inspection of the dataset structure
* summary statistics and missing value checks
* a histogram showing the distribution of points per game
* a line graph showing average points per game by season
* a scatterplot showing the relationship between usage percentage and points per game
* joined-data summaries using conference and division information

The reasoning behind these steps is to move from basic understanding of the dataset to more meaningful interpretation of patterns and relationships.

---

## Key Outputs

This repository includes:

* an exploratory analysis notebook of NBA player statistics
* exported HTML and Markdown notebook versions
* a joined dataset with conference and division information
* summary tables saved in the `results/` folder
* saved figures showing distribution, trends over time, and variable relationships

---

## Note on Data

Raw data files are excluded from GitHub using `.gitignore`.

This was done to keep the repository cleaner and to separate raw input data from processed and documented project outputs.

---

## AI Use

AI was used to help with troubleshooting, project organization, documentation planning, clarifying Git/GitHub steps, and some code assistance. Final review, decisions, and edits were completed by me.
