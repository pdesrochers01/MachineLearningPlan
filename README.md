This checklist can guide Data scientist through Machine Learning projects.

# Frame the Problem and Look at the Big Picture
1. Define the business objectives.
1. Identify Use cases.
1. Identify the current solutions/workarounds (if any).
1. Identify possible ML solutions (supervised/unsupervised, online/offline, etc.)
1. Identify KPI (aligned with the business objective).
1. Identify the minimum performance needed to reach the business objective.
1. Search for comparable problems (to reuse experience or tools).
1. Assign resources (find available expertise).
1. Identify how to solve the problem manually.
1. List assumptions and risks.
1. Verify assumptions if possible.

# Get the Data
*Note: automate as much as possible so we can easily update data when needed.*
1. List the data we need and how much we need.
1. Find and document where we can get that data.
1. Validate how much space it will take.
1. Check legal obligations and get access authorization if necessary.
1. Validate all access authorizations are working.
1. Create workspaces (with enough storage space).
1. Get the data.
1. Convert the data to a format we can easily manipulate (without changing the data itself).
1. Ensure sensitive information is deleted or protected (e.g., anonymized).
1. Validate the size and type of data (time series, sample, geographical, etc.).
1. Sample a test set and store it aside (to validate the model).

# Explore the Data
*Note: SME are required to get insights for these steps.*
1. Create a subset copy of the data for exploration.
1. Create a Jupyter notebook to keep a record of your data exploration.
1. Study each attribute and its characteristics:
  - Name
  - Type (categorical, in/float, bounded/unbounded, text, structured, etc.)
  - % of missing values
  - Noisiness and type of noise (stochastic, outliers, rounding errors, etc.)
  - Usefulness for the task
  - Type of distribution (Gaussian, uniform, logarithmic, etc.)
1. For supervised learning tasks, identify the target attribute(s).
1. Analyze correlations between attributes.
1. Analyze how to solve the problem manually (if possible).
1. Identify extra data that would be useful.
1. Document what we have learned.

# Prepare the Data
*Notes:*
- We should always work on copies of the data (keep the original dataset intact).
- We must write functions for all data transformations we apply, for these reasons:
  - So we can easily prepare the data the next time we get a fresh dataset
  - So we can apply these transformations in future projects
  - To clean and prepare the test set
  - To clean and prepare new data instances once our solution is live
  - To make it easy to treat our preparation choices as hyperparameters*
1. Data cleaning:
  - Fix or remove outliers.
  - Fill in missing values (e.g., with zero, mean, median, etc.) or drop their rows (or columns).
  - Drop the attributes that provide no useful information for the task.
1. Feature engineering, where appropriate:
  - Decompose features (e.g., categorical, date/time, etc.)
  - Enhance features (e.g., log(x), sqrt(x), x square, etc.)
  - Aggregate features into promising new features.
  - Standardize or normalize features.

Shortlist Promising Models
*Notes:*
- If the data is huge, we should sample smaller training sets so we can train many different models in a reasonable time.
- Automate these steps as much as possible.
1. Train many quick-and-dirty models from different categories (e.g., linear, naive Bayes, SVM, Random Forest, neural using standard parameters.
1. Measure and compare their performance.
- For each model, use N-fold cross-validation and compute the mean and standard deviation of the performance measure on the N folds.
1. Analyze the most significant variables for each algorithm.
1. Analyze the types of errors the models make.
- What data would a human have used to avoid these errors?
1. Perform a quick round of feature selection and engineering.
1. Perform one or two more quick iterations of the five previous steps.
1. Shortlist the top three to five most promising models, preferring models that make different types of errors.

Fine-Tune the System
Notes:
•	You will want to use as much data as possible for this step, especially as you move toward the end of fine-tuning.
•	As always, automate what you can.

1. Fine-tune the hyperparameters using cross-validation:
•	Treat your data transformation choices as hyperparameters, especially when you are not sure about them (e.g., if you're not sure whether to replace missing values with zeros or with the median value, or to just drop the rows).
•	Unless there are very few hyperparameter values to explore, prefer random search over grid search. If training is very long, you may prefer a Bayesian optimization approach.
2. Try Ensemble methods. Combining your best models will often produce better performance than running them individually.

3. Once you are confident about your final model, measure its performance on the test set to estimate the generalization error. Don't tweak your model after measuring the generalization error: you would just start overfitting the test set.

Present Your Solution

1. Document what you have done.

2. Create a nice presentation.
•	Make sure you highlight the big picture first.

3. Explain why your solution achieves the business objective.

4. Don't forget to present interesting points you noticed along the way.
•	Describe what worked and what did not.
•	List your assumptions and your system's limitations.

5. Ensure your key findings are communicated through beautiful visualizations or
easy-to-remember statements (e.8., "the median income is the number-one predictor of housing prices").

Launch!

1. Get your solution ready for production (plug into production data inputs, write
unit tests, etc.).

2. Write monitoring code to check your system's live performance at regular intervals and trigger alerts when it drops.
•	Beware of slow degradation: models tend to "rot" as data evolves.
•	Measuring performance may require a human pipeline (e.g., via a crowdsourcing service).
•	Also monitor your inputs' quality (e.g., a malfunctioning sensor sending random values, or another team's output becoming stale). This is particularly
important for online learning systems.

3. Retrain your models on a regular basis on fresh data (automate as much as
possible
