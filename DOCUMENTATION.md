## Project Overview
This project focused on analyzing electric vehicle (EV) registration data in Washington State to generate key insights using a data pipeline. I approached the challenge by first exploring and cleaning the raw CSV dataset, then modeling the data into a structured SQL database using SQLite, and finally performing multiple queries and visualizations to uncover trends.

The main challenges included:

* **Handling inconsistent column names** in the original dataset, which required renaming for clarity and usability.
* **Managing missing and malformed data**, especially in numerical fields like `Model_Year`, `Electric_Range`, and `Base_MSRP`. I solved this by coercing invalid entries into NaN and dropping incomplete records only when necessary.I decided to drop these rows because they did not represent a significant or representative portion of the dataset, and their absence did not compromise the quality or integrity of the analysis.
* **Designing meaningful visualizations** that could highlight trends in EV adoption across years, models, and counties without overwhelming the user with too much data.


---

## Architecture, Design Decisions, and Data Transformations

### Architecture Overview:

* **Language & Tools**: Python (Pandas, Seaborn, Matplotlib, SQLAlchemy)
* **Storage**: Local SQLite database created using `sqlalchemy.create_engine`. SQLite was chosen because it is lightweight, easy to set up, and well-suited for small to medium-sized datasets like this one. It allowed for quick querying without the overhead of configuring a more complex database system.
* **Visualization**: Seaborn & Matplotlib for intuitive data representation
* **Execution Environment**: The entire pipeline was run locally due to the manageable size of the dataset, which made using a cloud-based or distributed solution unnecessary. Running locally also ensured faster iterations during development.


### Design & Logic:

1. **Data Ingestion**:

   * Used `pandas.read_csv()` to load the dataset.
   * Cleaned column names for readability and consistency.

2. **Data Cleaning**:

   * Dropped rows with null values in critical fields (`Model_Year`, `Model`, `County`). This decision was made because the removed rows accounted for less than 5% of the dataset. In other words, they were not significant or representative enough to impact the overall results or conclusions.
   * Converted string-based numeric fields to actual numerical types with error handling.

3. **Data Transformation & Modeling**:

   * Stored the cleaned DataFrame in a local SQLite database.
   * Used raw SQL queries to compute:

     * Registrations per year.
     * Top 10 most registered EV models.
     * Counties with highest CAFV-eligible vehicle concentrations.
     * County-wise year-over-year trends.

4. **Visualization**:
   * To enhance the analysis, results were presented visually — after all, a chart is worth a thousand words.
   * Created bar plots and line plots to visualize each query’s output.
   * Used `sns.set(style='whitegrid')` for a clean, readable chart style.
   * Filtered top counties and limited results to post-2010 to ensure clarity and relevance.