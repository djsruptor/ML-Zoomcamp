# Definition

Machine learning is the process of extracting patterns from data to predict a target value.

Data is split into two types of data:
- Features: Information about the object that may be related to the target variable
- Target: Property we're trying to predict

### Example

Machine Learning models are widely used to predict car prices in a dealer, some of the features they may use are year, mileage, brand; the target value will be price of the car. 

The model uses historical data to learn the influence of these variables in the car's price, so when new cars are logged into the system, it can predict its price.

# Differences between ML and Rule-based systems

- Rule-based systems created manually with low code that need a lot of mantainance because they are very specific.
- Machine Learning systems use rules defined by the user to define and calculate features, which are used to train the model and make predictions of a target variable.

### Example

The user sets a rule-based system that classifies as SPAM all emails that include the word "Offer", then receives an email from their boss with a new job offer; the system classifies it as spam so the user needs to update it and exclude emails from his boss. This cycle will keep happening with many specific scenarios. 
A machine learning model gets the data from the users' email history, calculates the features defined by the developer using the rules defined by the user, such as "length of subject", "length of email body", "sender's domain"; trains/fits the model by analyzing how these features influence the target; it's used to predict the probability of emails being spam; finally these probabilities are used to make decisions (If P>= 0.5, classify as spam, else, "Good message")

# Supervised Machine Learning

When training a supervised model, the input data includes examples of the target values. The idea is to teach the model how to predict a value.

The notation for supervised machine learning models is $g(X)≈Y$. 
- g represents the model, X represents the features, and Y represents the target. 
- The goal is to apply a statistical model (g) that uses the known features (X) to get an approximate value of the target (Y).

There are many types of Supervised ML models:
- Regression: Expected output is a number
- Classification: Expected output is a category
    - Multiclass classification: Expects a classification in a set number of categories.
    - Binary: There are two options of categories
- Ranking: The expected output is a scoring system ranked from best to worst and filter by top N.

### Regression example: Car price ML model

Features are the following values:
- Year
- Mileage
- Brand

Target is the following predicted value:
- Price

|Features              | Target  |
|----------------------|---------|
| [2020, 100000, Ford] | $30.000 | 
| [2010, 1000000, Ford] | $10.000 | 
| [2020, 100000, BMW] | $60.000 |
| [2010, 1000000, BMW] | $15.000 |  

### Classification example: Spam classification ML model

Features are the following booleans:
- Subject longer than 10 characters?
- Sender domain is online.com?
- Mentions the word "Offer"?

Target is boolean for:
- Is spam?

|Features              | Target  |
|----------------------|---------|
| [1, 1, 1] | 0.95 | 
| [1, 0, 1] | 0.4 | 
| [0, 0, 1] | 0.32 |
| [0, 1, 1] | 0.81 |  

### Ranking example: Amazon recommendation system

Features are the following values:
- Last search
- Location
- Platform

Target is descending ranking of the following items:
- Iphone case
- Headphones
- Android charger
- Bycicle
- Trekking shoes

|Features              | Target  |
|----------------------|---------|
| [Iphone, Colombia, IOS] | [0.9, 0.85, 0.4, 0.1, 0.15] | 
| [Football, Colombia, IOS] | [0.4, 0.6, 0.2, 0.7, 0.6] |
| [Winter jacket, Colombia, IOS] | [0.21, 0.73, 0.4, 0.83, 0.9] |
| [Android charger, Colombia, IOS] | [0.26, 0.85, 0.97, 0.33, 0.25] |

# CRISP-DM: Main Stages

CRISP-DM (Cross-Industry Standard Process for Data Mining) is a methodology for organizing ML projects. 
ML projects require many iterations: Start with simple models, so we can learn from users feedback and improve them. 

It consists of four main stages:

1. **Understand the problem**
2. **Collect the data**
3. **Train the model**
4. **Use it**

---

### 1. Understand the Problem

- **Goal:** Identify the problem to solve, how it can be solved, and define the measure of success.
- **Key questions:**
    - Is machine learning required for this problem?
    - How many users are impacted?
    - Is ML the best approach?
- **Example:**  
  Users are complaining about spam in their mailboxes.
    - Goal: Reduce the amount of spam messages or complaints about spam.
    - The goal must be measurable, e.g., "Reduce the amount of spam messages by 50%".

---

### 2. Data Understanding

- **Goal:** Analyze available data to decide if more data is needed.
- **Steps:**
    - Identify data sources (e.g., spam report button).
    - Assess data reliability and tracking.
    - Check if the dataset is large enough to train a model.
    - Identify any missing data.
- **Note:**  
  Insights from this step may require revisiting the business understanding phase.

---

### 3. Data Preparation

- **Goal:** Transform data for use in training a machine learning model.
- **Actions:**
    - Clean the data.
    - Build data processing pipelines.
    - Convert data into a suitable format (e.g., tabular/SQL).

---

### 4. Modeling

- **Goal:** Train and select the best-performing model.
- **Actions:**
    - Train different models (e.g., regression, decision tree, neural network).
    - Perform additional data preparation as needed (add features, fix issues).
    - Measure model effectiveness: Has the goal been reached for the test group?

---

### 5. Evaluation & Deployment

- **Goal:** Assess if the model meets the business goal and deploy if successful.
- **Actions:**
    - Retrospective analysis: Was the goal achievable? Was the approach optimal?
    - Adjust the goal, deploy the model, or halt the project as needed.
    - Online evaluation: Deploy to a small sample of users (e.g., 5%) and evaluate.
    - If successful, roll out to all users.
    - Ensure monitoring for quality and maintainability.
    - Iterate and improve the model based on business needs.
    - Finally we roll the model to production for all users.

# Model Selection Process

In ML projects, it is a common practice to run multiple types of models, score them and compare their results to select the best one.

To achieve this validation, we split the data into three subsets: Training (60%), Validation (20%), Testing (20%).

|Train 60%|Validate 20%|Test 20%|

To identify the best model we need to create a comparison chart, and the best metric to compare is **accuracy** ($\frac{(Successful Ŷ_v - Total Y_v)}{(Total Y_v)}$).

After selecting the model with the highest performance on the validation data, we run it on the testing data to confirm the best model is consistent.

#### Validation chart
|Model|Accuracy|
|-----|--------|
|LR|60%|
|DT|61%|
|RF|67%|
|NN|__80%__|

Neural Network is run on the testing data and returns 79% of accuracy. It shows consistent results and can be rolled to production.

The model selection process follows these steps:
1. Split the data
2. Train the model
3. Validate the model
4. Select the best model
5. Test the selected model
6. Check the model's performance is consistent


### Example
The model defined to filter spam emails returns a 57% of probability of accurately detecting spam in its first badge. 

#### Accuracy validation for binary classification model
|$P(Ŷ_v)$|$Ŷ_v$|$Y_v$|val|
|-|-|-|-|
|0.8 | 1|1|G|
|0.7 | 1|1|G|
|0.6 | 1|1|G|
|0.1 | 0|1|B|
|0.9 | 1|0|B|
|0.6 | 1|0|B|
|0.2 | 0|0|G|

This must be done for all the models to compare

#### Validation chart
|Model|Accuracy|
|-----|--------|
|BC|57%|
|DT|**61%**|
|MC|38%|
|NN|25%|

In this case, the best performing model was the __Decision Tree__, so we run it on the testing data to confirm:

#### Accuracy test for decision tree model
|$Ŷ_t$|$Y_t$|check|
|-|-|-|
|0|1|B|
|1|1|G|
|1|1|G|
|0|1|B|
|0|0|G|
|0|0|G|
|1|0|B|

The accuracy of the model in the testing phase was 57%, close enough to the original performance, so we are confident about its consistency over time.