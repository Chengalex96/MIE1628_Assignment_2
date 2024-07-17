# MIE1628_Assignment_2
 
Done using Pyspark

Part A:

Question 1: Count the number of odd and even numbers from the file's 'integer.txt' using Pyspark

Pyspark allows us to separate the data into partitions to be able to calculate faster. Need to initialize a spark session. 

Question 2: Calculate the salary sum per department using Pyspark

Convert the csv file into a spark file, rename columns, groupby departments, and sum them up

Question 3: Implement MapReduce using Pyspark to find out how many times specific words appear from a Shakespeare txt file that are also case-sensitive

counts = book.flatMap(lambda line: line.split(" ")) \
             .map(lambda word: (word, 1)) \
             .reduceByKey(lambda a, b: a + b)

Question 4: Calculate the top 10 and bottom 10 words of Shakespeare txt based on the frequency

Convert all words to lowercase to avoid case sensitivity:

   def lower_clean_str(x):
   
     punc='!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
     
     lowercased_str = x.lower()
     
     for ch in punc:
     
       lowercased_str = lowercased_str.replace(ch, '')
       
     return lowercased_str

Part B: Create a recommender system using Apache Spark

The data is sorted by user (labelled 0-29), in which they provide a rating (1-5) for a specific movie (labelled 1-99) and lists every movie they rated. 

Displaying the top 20 movies with the highest (most numbers) rating

Displaying the top 15 users who provided the highest (most number of) ratings

Split data set into train and test and use collaborative filtering approach, this will recommend movies based on similar users

Using Pyspark ML to fit training data using RMSE and MAE

MAE is Mean Absolute Error, it calculates the absolute distance between the dataset and its prediction on  a regression and takes the average over all the observations. 

MSE is Mean Squared Error, similar to MAE but squares the distance to take account of the negatives. Higher errors weigh/contribute more to the scale, although you are provided squared units, which may not always make sense.

RMSE is Root Mean Squared Error, this returns the MSE error to the original unit by taking the square root, while still penalizing higher errors

Which metrics work better depends on the scenario, RMSE works better at detecting outliers which may be more useful in this case since you do not want to recommend an outlier movie to a user (for example, a horror movie to a kid), there's also multiple movies being recommended to the user so the user will have multiple selections

Parameter Gridbuilder to sort through the best parameters:

parameters_tuned=ParamGridBuilder()\
.addGrid(als.rank,[10, 50])\
.addGrid(als.maxIter, [10, 15])\
.addGrid(als.regParam, [0.01, 1.0])\
.build()

Best Model Parameters:
Rank: 50
MaxIter: 15
RegParam: 0.01

Calculate the top 15 movie recommendations for user id 10 and user id 14.

![image](https://github.com/user-attachments/assets/6ba4672f-07a7-41c7-b655-84ded6f47db8)

