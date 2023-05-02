Download Link: https://assignmentchef.com/product/solved-cmsc-435-assignment-2
<br>
This assignment asks you to implement and evaluate four algorithms for the imputation of missing values using two provided datasets. You will also evaluate and compare quality of the imputed values by comparing them with the corresponding values in the “complete” dataset.




<h1>Datasets</h1>

There are three datasets: the original dataset without missing values and two derived datasets where the missing values were introduced at two different amounts:

<ul>

 <li><em>csv</em> file is the complete dataset. It includes 9 features (including the class/predicted features) and 8795 objects.</li>

 <li><em>csv</em> and <em>dataset_missing20.csv </em>files include the same dataset with 5% and 20% of missing values, respectively.</li>

</ul>

You will impute the missing values in each of the latter two datasets and compare these imputed values to the true/correct values that are available in the <em>dataset_complete.csv</em> file to evaluate and compare quality of different imputation algorithms. The three files are in the comma separated value (CSV) format. The first line in each file defines the names of features and the remaining lines include the values of the corresponding 8795 objects. The first 8 features are numeric and continuous with values in [0, 1] interval. The last, class feature is symbolic and binary with values Yes and No. The missing values are represented by ?. There are no missing values in the class feature.




<h1>Algorithms for missing data imputation</h1>

You will implement four algorithms for the imputation of missing values and apply each of them on the corresponding two datasets that have missing values: <em>dataset_missing05.csv</em> and <em>dataset_missing20.csv</em>.

<em> </em>

<h2>Algorithm 1. Mean imputation</h2>

Missing value for a specific feature and object is imputed with the mean value computed using the complete values of this feature.

<strong> </strong>

Example<strong>  </strong>

<table width="340">

 <tbody>

  <tr>

   <td width="93">F1</td>

   <td width="92">F2</td>

   <td width="92">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="93">0.40256</td>

   <td width="92">0.14970</td>

   <td width="92">?</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="93">0.41139</td>

   <td width="92">0.30140</td>

   <td width="92">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">0.24752</td>

   <td width="92">0.32148</td>

   <td width="92">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="93">0.24609</td>

   <td width="92">?</td>

   <td width="92">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">?</td>

   <td width="92">0.58306</td>

   <td width="92">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>




Object 1

Object 2 Object 3 Object 4

Object 5

To impute the missing value for feature F3 from object 1, we compute the mean of all complete values of F3: <em>mean</em> = (0.11169 + 0.13986 + 0.0891) / 3 = 0.11355.

<table width="340">

 <tbody>

  <tr>

   <td width="93">F1</td>

   <td width="92">F2</td>

   <td width="92">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="93">0.40256</td>

   <td width="92">0.14970</td>

   <td width="92">0.11355</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="93">0.41139</td>

   <td width="92">0.30140</td>

   <td width="92">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">0.24752</td>

   <td width="92">0.32148</td>

   <td width="92">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="93">0.24609</td>

   <td width="92">?</td>

   <td width="92">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">?</td>

   <td width="92">0.58306</td>

   <td width="92">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>




Object 1

Object 2 Object 3 Object 4

Object 5

The imputed values <strong>must not</strong> be used to compute the means. This means that all missing values for a given feature are imputed with the same mean value.

<table width="340">

 <tbody>

  <tr>

   <td width="93">F1</td>

   <td width="92">F2</td>

   <td width="92">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="93">0.40256</td>

   <td width="92">0.14970</td>

   <td width="92">0.11355</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="93">0.41139</td>

   <td width="92">0.30140</td>

   <td width="92">0.11355</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">0.24752</td>

   <td width="92">0.32148</td>

   <td width="92">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="93">0.24609</td>

   <td width="92">?</td>

   <td width="92">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">?</td>

   <td width="92">0.58306</td>

   <td width="92">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>




Object 1

Object 2 Object 3 Object 4

Object 5

<h2>Algorithm 2. Conditional mean imputation</h2>

Missing value for a specific feature and object is imputed with the mean value computed using the complete values of this feature for objects that satisfy a condition defined by the class feature. For instance, a missing value for an object 1 for which class = No is imputed based on the mean value computed using all objects for which class = No.

Example

<table width="340">

 <tbody>

  <tr>

   <td width="93">F1</td>

   <td width="92">F2</td>

   <td width="92">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="93">0.40256</td>

   <td width="92">0.14970</td>

   <td width="92">?</td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="93">0.41139</td>

   <td width="92">0.30140</td>

   <td width="92">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">0.24752</td>

   <td width="92">0.32148</td>

   <td width="92"><strong>0.11169 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="93">0.24609</td>

   <td width="92">?</td>

   <td width="92">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">?</td>

   <td width="92">0.58306</td>

   <td width="92"><strong>0.08910 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

 </tbody>

</table>




Object 1

Object 2

Object 3

Object 4

Object 5

For object 1 for which class = No, the missing value for the feature F3 is imputed as <em>mean</em><sub>No</sub> = (0.11169 + 0.0891) / 2 = 0.10039

For object 2 for which class = Yes, the missing value for the feature F3 is imputed as <em>mean</em><sub>Yes</sub> = 0.13986 / 1 = 0.13986 The two imputed values are

<table width="340">

 <tbody>

  <tr>

   <td width="93">F1</td>

   <td width="92">F2</td>

   <td width="92">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="93">0.40256</td>

   <td width="92">0.14970</td>

   <td width="92"><strong>0.10039 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="93">0.41139</td>

   <td width="92">0.30140</td>

   <td width="92">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">0.24752</td>

   <td width="92">0.32148</td>

   <td width="92"><strong>0.11169 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="93">0.24609</td>

   <td width="92">?</td>

   <td width="92">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="93">?</td>

   <td width="92">0.58306</td>

   <td width="92"><strong>0.08910 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

 </tbody>

</table>




Object 1

Object 2

Object 3

Object 4

Object 5

<h2>Algorithm 3. Hot deck imputation</h2>

Missing values for features that have missing values in a given object are imputed with the values for the same features copied from another, the most similar object. First, similarity of a given object that has missing values with every other object in the dataset is computed using the Euclidean distance. The object with the smallest distance is assumed to be the most similar and its values are used for the imputation. If that object is missing some of the values that should be imputed then the second most similar object is used to impute the remaining missing values, and so on. In other words, you should use the first complete value that you find by screening objects by their increasing values of the distance.

Given two objects <strong>x           </strong>,     , …    , … ,      and <strong>y           </strong>,    , … ,    , … ,      , the Euclidean distance is

calculated as      <strong>x, y       </strong> where     and      are values of feature <em>i</em> for objects <strong>x</strong> and <strong>y</strong>,

respectively,  is the number of features (excluding the class future), and       ≤  is the number of features that do not have missing values in either of the two objects. In other words, the distance is computed using the <em>m</em> features that have complete values. Note that you <strong>must not </strong>use the class feature in the calculation of the distance.

Example

<table width="304">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="80">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="80">?</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="80">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="80">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">?</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">?</td>

   <td width="80">0.58306</td>

   <td width="80">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>




Object 1

Object 2 Object 3 Object 4

Object 5

To impute missing value for feature F3 from object 1, we compute distances to every other object

1,        2 0.40256 0.41139     0.1497             0.3014           /2     0.0760

1,        3 0.40256 0.24752     0.1497            0.32148           /2      0.1157

1,        4 0.40256 0.24609          /1      0.1565

1,        5 0.1497 0.58306          /1      0.4334

Since object 2 that is the most similar to object 1 has a missing value for the feature F3, the second nearest object 3 is used and the missing value is imputed as follows




<table width="304">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="80">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="80">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="80">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="80">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">?</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">?</td>

   <td width="80">0.58306</td>

   <td width="80">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>




Object 1

Object 2 Object 3 Object 4

Object 5

The imputed values <strong>must not</strong> be used to compute the distances. In other words, all missing values for each feature are imputed based on the distances that use the dataset before the imputation. This ensures that the errors inherent in the imputed values are not propagated to compute the imputation.

<h2>Algorithm 4. Conditional hot deck imputation</h2>

Missing values for features with missing values in a given object are imputed with the values for the same features copied from another, most similar object that satisfies a condition defined by the class feature. For instance, a missing value for an object 1 for which class = No is imputed based on similarity only to the objects for which class = No. The calculation of the similarities follows the unconditional hot deck imputation.

Example

<table width="304">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="80">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="80"><strong>? </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="80">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="80"><strong>0.11169 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">?</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">?</td>

   <td width="80">0.58306</td>

   <td width="80"><strong>0.08910 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

 </tbody>

</table>




Object 1

Object 2

Object 3

Object 4

Object 5




To impute missing value for feature F3 from object 1, we first compute the two distances to the objects that share the same value of the class feature

1,        3 0.40256 0.24752     0.1497            0.32148           /2      0.1157

1,        5 0.1497 0.58306          /1      0.4334

The missing value is imputed with the value for the same feature F3 from the closest object 3 as follows.

<table width="304">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="80">F3</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="80"><strong>0.11169 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="80">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="80"><strong>0.11169 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">?</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">?</td>

   <td width="80">0.58306</td>

   <td width="80"><strong>0.08910 </strong></td>

   <td width="64"><strong>No </strong></td>

  </tr>

 </tbody>

</table>




Object 1

Object 2

Object 3

Object 4

Object 5

Like for the unconditional hot deck imputation, the imputed values <strong>must not</strong> be used to compute the distances.




<h1>Calculation of the imputation error</h1>

You will use the two datasets that were imputed with the four methods to calculate the corresponding eight imputation errors. You will evaluate quality of these imputations based on the Mean Absolute Error (MAE) between the imputed values and the corresponding complete values that are available in the <em>dataset_complete.csv</em> file. This dataset should be used only to calculate MAE values, not to perform the imputations. The MAE values should be used to judge and compare the quality of each imputation.

Given the imputed values<strong> x    </strong>,           , …       , … ,      computed from a dataset that has missing values and the corresponding complete values <strong>t        </strong>,           , … ,      , … ,      in the complete dataset, MAE is defined as

1

|           |

where    is the total number of missing values,            is a the imputed value in the dataset that has missing values,  and  are values for the same object and same feature in the two datasets, and |       ∙           | denotes the absolute value.

<table width="385">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="81">F3</td>

   <td width="80">F4</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="81">0.16870</td>

   <td width="80">?</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="81">0.47033</td>

   <td width="80">?</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="81">0.41167</td>

   <td width="80">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">?</td>

   <td width="81">?</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">?</td>

   <td width="80">0.58306</td>

   <td width="81">0.52568</td>

   <td width="80">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>

Example Incomplete dataset

Object 1

Object 2 Object 3 Object 4

Object 5




<table width="385">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="81">F3</td>

   <td width="80">F4</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="81">0.16870</td>

   <td width="80">0.11355</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="81">0.47033</td>

   <td width="80">0.11355</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="81">0.41167</td>

   <td width="80">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">0.33891</td>

   <td width="81">0.39409</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.32689</td>

   <td width="80">0.58306</td>

   <td width="81">0.52568</td>

   <td width="80">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>

Dataset where values  were imputed using Object 1

Object 2

the unconditional     Object 3 mean imputation          Object 4

Object 5




<table width="385">

 <tbody>

  <tr>

   <td width="80">F1</td>

   <td width="80">F2</td>

   <td width="81">F3</td>

   <td width="80">F4</td>

   <td width="64">Class</td>

  </tr>

  <tr>

   <td width="80">0.40256</td>

   <td width="80">0.14970</td>

   <td width="81">0.16870</td>

   <td width="80">0</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.41139</td>

   <td width="80">0.30140</td>

   <td width="81">0.47033</td>

   <td width="80">0.14175</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.24752</td>

   <td width="80">0.32148</td>

   <td width="81">0.41167</td>

   <td width="80">0.11169</td>

   <td width="64">No</td>

  </tr>

  <tr>

   <td width="80">0.24609</td>

   <td width="80">0.21359</td>

   <td width="81">0.24071</td>

   <td width="80">0.13986</td>

   <td width="64">Yes</td>

  </tr>

  <tr>

   <td width="80">0.70541</td>

   <td width="80">0.58306</td>

   <td width="81">0.52568</td>

   <td width="80">0.08910</td>

   <td width="64">No</td>

  </tr>

 </tbody>

</table>

Complete dataset          <sup> </sup>

Object 1

Object 2 Object 3 Object 4

Object 5 <strong> </strong>

Given the above imputation, the MAE is calculated as follows.

|0.11355     0|     |0.11355     0.14175|     |0.33891     0.21359|

|0.39409     0.24071|     |0.32689     0.70541|      0.1598

The MAE values must be computed with precision of <strong>four digits</strong> after the decimal point.

The imputed values must be computed with precision of <strong>five digits</strong> after the decimal point.




<h1>Implementation</h1>

Your code must perform imputation, display the eight values of MAE on the screen and save the eight imputed datasets in the csv format. The imputed datasets should be named as follows: <em>Vnumber_missing05_imputed_mean.csv</em>

<em>Vnumber_missing05_imputed_mean_conditional.csv</em>

<em>Vnumber_missing05_imputed_hd.csv</em>

<em>Vnumber_missing05_imputed_hd_conditional.csv</em>

<em>Vnumber_ missing20_imputed_mean.csv</em>

<em>Vnumber_missing20_imputed_mean_conditional.csv</em>

<em>Vnumber_missing20_imputed_hd.csv</em>

<em>Vnumber_missing20_imputed_hd_conditional.csv</em>

where <em>Vnumber</em> is your V number, e.g., <em>V12345678_missing01_imputed_mean.csv</em>




The MAE values should be displayed on the screen in the following format




<em>MAE_05_mean = 0.1234 </em>

<em>MAE_05_mean_conditional = 0.5678 </em>

<em>MAE_05_hd = 0.1234 </em>

<em>MAE_05_hd_conditional = 0.5678 </em>

<em>MAE_20_mean = 0.1234 </em>

<em>MAE_20_mean_conditional = 0.5678 </em>

<em>MAE_20_hd = 0.1234 </em>

<em>MAE_20_hd_conditional = 0.5678 </em>




You must use Java or Python3 to implement all computations including loading the datasets from the csv files, coding the four imputation methods, calculation of the MAE values, printing the MAE values on the screen, and saving of the eight imputed datasets. You may use multiple classes and functions, but they must be included in <strong>a single source code (.java or .py) file</strong>. This java/python file must successfully compile and produce the above mentioned outputs. Make sure to use appropriate data types to ensure the required precision of results. If you use Java then make sure that the program can be run using the following commands: javac a2.java java a2

This means that your main class should be named a2 and you should not specify a package in your code. If you use Python3 then make sure that the program can be run using the following command: python a2.py

In both cases the program should expect that the three input csv files are located in the same working directory from which the code is run.


