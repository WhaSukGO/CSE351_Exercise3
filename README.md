# Predict Black Friday Sales
In this exercise, you will solve a data challenge as a group project using the following approach: 	
1) Visit the data challenge page. 
2) Read carefully the problem to be solved. 
3) Download dataset. 
4) Figure out suitable approaches for solving the problem. 
5) Preprocess data for creating a dataset suitable for experimentation. 
6) Use your favorite data analysis tool to solve the problem. 
7) Report the approach taken, steps for using your favorite data analysis tool and your results in a PPT format and submit on Blackboard. 
8) Create a Github repository, upload your preprocessed data, steps for using your favorite data analysis tool and your results. Submit the Github link on blackboard.
## Contributor
- Wha Suk Lee
- Haein Park
- Pyungkang Hong
## Tools
- KNIME 4.1.0
## Data
| Variable | Definition |
|--|--|
|User_ID |User ID|
|Product_ID|Product ID|
|Gender|Sex of User|
|Age|Age in bins|
|Occupation|Occupation (Masked)|
|City_Category|Category of the City (A,B,C)
|Stay_In_Current_City_Years|Number of years stay in current city
|Marital_Status|Marital Status
|Product_Category_1|Product Category (Masked)
|Product_Category_2|Product may belongs to other category also (Masked)
|Product_Category_3|Product may belongs to other category also (Masked)
|Purchase|Purchase Amount (Target Variable)

## Preprocessing
There are some missing values found in columns,
- Stay_In_Current_City_Years
- Product_Category_2
- Product_Category_3

Two naive approaches are suggested to remove missing values in category columns
1) Why not remove unnecessary categories?

2) If any missing value is found, replace it with the upper category.

To remove missing values in "Stay_In_Current_City_Years" column
	
1) Replace missing values with zeros

  
## Nodes

### Column Filter
![Column Filter](/assets/Column_filter.png)

Removes selected columns, such as Product_Category_ 2 and 3, in the table.

### Missing Value
![Missing Value](/assets/Missing_value.png)

Using regular expressions or conditions, replace missing values with specific values. It is used to replace missing values with zeros in "Stay_In_Current_City_Years" column

### Rule Engine
![Rule Engine](/assets/Rule_engine.png)

Use conditions to update specific attributes in a row. If any missing value is found in category columns, replace it with the upper category. (For example, if Product_Category_2 has no value, replace it with the value of Product_Category_1)

## Regression Models

![Regression Models](/assets/Regression_models.png)

1) Polynomial Regression Learner (max degree of 3)
	Polynomial Regression Learner is a form of linear regression in which the relationship between the input variables x and the output variable y is modeled as a polynomial. Although polynomial regression fits a nonlinear model to the data, as a statistical estimation problem it is linear, in the sense that the regression function is linear in the unknown parameters that are estimated from the data. For this reason, polynomial regression is considered to be a special case of linear regression.polynomial regression equation is y= b0 + b1x + b2x^2+… it helps to minimize the squared error of the coeffient b attached to the front It minimize the distance between points and lines. Input ports type is data, output ports tpyes are PMML and data. 
	
2) Linear Regression Learner
	Learns a single regression tree. The procedure follows the algorithm described by "Classification and Regression Trees" 
In the Perform Multivariate Linear Regression dialog box, select the destination column (the combo box at the top), that is, the response. It only include specific columns that represent (independent) variables using two lists in the center of the dialog box.
The Options are Target, values, Predefined Offset, Value, Missing Values in Input Data, Scatter Plot View.

3) Simple Regression Tree Learner
	The treatment of missing values currently used is also different from the value used. In each division, the algorithm tries to find the best direction for missing values by transferring values in each direction and choosing the value that yields the best results (i.e., the greatest gain). Learns a single regression tree. The procedure follows the algorithm described by "Classification and Regression Trees" Attribute Selection Options are Target Column, Trribute selection, Ignore columns without domain information, Enable Hightlighting , Missing value hnding, Limit number of levels, Minium split node size, minimum node size 
Inpute ports type is Data (Simple Regression Tree predictor) Output ports type is regression tree  (Simple Regression Tree Predictor)

## Test Results (Accuracy)

The lower the result, the more accurate the model is!

PR: Polynomial Regression<br/>
LR: Linear Regression<br/>
RT: Regression Tree

### Column-Removed Training Data

Test 1-PR_CE: 4258.26486987406<br/>
Test 2-LR_CE: 4711.838698231092<br/>
Test 3-RT_CE: 3044.0250955813617

### Missing Value Replaced Data

Test 4-PR_MV: 4244.682192134847<br/>
Test 5-LR_MV: 4591.672720036235<br/>
Test 6-RT_MV: 3270.7834458726347

## Links
`<URL>` : <https://datahack.analyticsvidhya.com/contest/black-friday/#ProblemStatement><br/>
`<Course URL>` : <https://ppawar.github.io/Spring2020/CSE351-S20/Exercises/Exercise%203.pdf>
