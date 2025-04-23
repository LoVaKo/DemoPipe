
# Bronze → Silver → Gold Pipeline Architecture

This project follows a modern **data lakehouse pipeline** structure using the **bronze → silver → gold** layering pattern. This layered architecture helps break down complex data workflows into manageable, reusable stages.

---
### Bronze Layer: Raw Data Ingestion
🎯 **Goal**: Collect and store the raw data exactly as it comes in

🔧 **Tasks a data engineer performs:**
- Write Python or Spark code to pull data from a source (API, file, database)
- Validate basic connectivity (check API responses, handle errors)
- Convert the raw response (e.g. JSON) to a DataFrame
- Store the data in a raw Delta table (or Parquet/CSV in simpler setups)
- Include basic metadata (e.g. ingestion timestamp)

---

### Silver Layer - Clean and Structure the Data

🎯 **Goal**: Make the data clean, consistent, and usable for downstream tasks

🔧 **Tasks a data engineer performs**:
- Read from the bronze layer
- Flatten nested structures (e.g. explode arrays)
- Drop invalid or duplicate rows
- Convert data types to the correct formats (e.g., height as float)
- Rename columns for clarity or consistency
- Store result as a new dataset

---

### Gold Layer: Use-Case-Specific Output (BI or ML)

🎯 **Goal**: Build specific outputs for reporting or machine learning

🔧 **Tasks a data engineer performs for ML:**
- Read from silver dataset
- Perform feature engineering: select and transform relevant columns
- Prepare a label column for ML (e.g. Pokémon type)
- Train a model using MLlib (e.g., Logistic Regression)
- Write predictions + probabilities to a gold Delta table

🔧 **Tasks a data engineer performs for BI:**
- Read from silver dataset
- Group and aggregate data 
- Apply business logic 
- Join with enrichment data
- Format columns for consumption
- Write output to dataset in gold layer > this will be used by tools like PowerBI.

## Data Kitchen Analogy
| Layer       | Kitchen Analogy                          | Description                                                                 |
|-------------|-------------------------------------------|-----------------------------------------------------------------------------|
| 🟫 **Bronze**  | Raw ingredients from the market           | You’ve just brought home the groceries — unwashed, uncut, maybe messy.       |
| 🥈 **Silver**  | Prepped ingredients                      | You've washed the veggies, chopped the onions, measured your spices.         |
| 🥇 **Gold**    | Final dish, plated and ready to serve    | The cooked, seasoned, and beautifully plated dish — ready to eat or serve.   |

> - **Bronze** = messy but essential input
> - **Silver** = cleaned, usable components
> - **Gold** = the final product used in analysis or machine learning
