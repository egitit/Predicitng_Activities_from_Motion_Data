# Predicting Activities from Motion data
For my project I wanted to try and predict an individuals activity given their motion data over a period of 5 minutes.

# Description of the Data
There were 8 participants, divided equally between women and men. The participants were asked to perform 19 different activities in their own style and were not restricted on how the activities should be performed. For this reason, there are inter-subject variations in the speeds and amplitudes of some activities. 

## How the data was aquired
Each subject will wear a total of 45 sensors between their Torso, Arms, and Legs. The sensors were:
- x, y, z - accelerometers - which measures accelleration
- x, y, z - gyroscopes - which measures rotation
- x, y, z - magnetometers- which measures the directional change of a magnetic field

The Participants performed the following activities while wearing the sensors:
1. Sitting
2. Standing
3. Laying on back
4. Laying on right side
5. Ascending stairs
6. Desceding stairs
7. Standing still in an elevator
8. Moving around in an elevator
9. Walking in a parking lot
10. Walking on a treadmill (flat)
11. Walking on treadmill (inclined 15 degrees)
12. Running on a treadmill
13. Exercising on a stepper
14. Exercising on a cross trainer
15. Cycling on an exercise bike (horizontal)
16. Cycling on an exercise bike (vertical)
17. Rowing
18. Jumping
19. PLaying Basketball


# Data Ingestion
I started off by creating a dataframe with 1.14 million rows of data as each participants data was spread out over 142,500 rows of data for all . That lead to potentially making 1.14 million predictions instead of prediciting on chunks of time. To combat this I ended up adding a time column, which was in increments of .04 seconds for EDA as well as participant numbers in order to groupy a participant by activities. 

# EDA
Once the data was in a workable format I started to explore what the acitivty data looked like. I started to pick up that these data points seemed to gravitate towards the mean. I also noticed that the variance in data points could be a great indicator when trying to predicts a persons activity. The greator the variance, the greator the motion. 

# Pre-modeling
- I needed to create my own customized train_test_split function in order to split my data randomly on participants. The training set consisted of 6 particiapnts, while the testing set had 2.
- I needed to create my own cross validation function in order to test my models on every potential testing set combination. This function would ultimately return the scores for each testing set, the range of scores, and the average score of that models performance.

# Modeling / Feature Engineering and selection
Overall I created 9 separate models each leveraging different features in order to try and imrpove on my models accuracy. Each model sampled a minute at a time of a particiapnts activity. The models were as followed:
1. All the features mean data
2. Torso features mean data
3. Arms features mean data
4. Legs features mean data
5. A combination(1) of ceratin arms, legs, and torso mean data
6. A combination(2) of arms and legs mean data
7. the variance of all the features data
8. Legs (mean) & variance
9. Combo2 (arms & legs mean) & Variance

# Conclusion
After scoring my models, the Combo2 & Variance dataframe consistantly scored in the mid-to-high 90's with a score ranged that varied by 7-8.

# Future Work
I would have liked to incorporate more of my engineered features into a model for testing. Potentially leverage the min, max, median and summation statistics datafarmes in order to add more features to my modeling. 

# Data Source
All the data credit goes to Billur Barshan from the Department of Electrical and Electronics Engineering, Bilkent University, TR-06800 Bilkent, Ankara, Turkey. <br/>
- tel: (90-312) 290-2161 fax: (90-312) 266-4192 e-mail : billur`@'ee.bilkent.edu.tr
- url: www.ee.bilkent.edu.tr/~billur
- Kerem Altun, kerem.altun '@' kemerburgaz.edu.tr, kerem.altun '@' gmail.com
(link to dataset: https://archive.ics.uci.edu/ml/datasets/daily+and+sports+activities#)
