# Cryptocurrencies

This project uses unsupervised machine learning and its appropriate data preprocessing to cluster a cryptocurrency dataset into groups depending on their characteristics.

## Overview

The cryptocurrency dataset consists of 1253 entries with the following attributes:

* Coin Name 
* Algorithm
* Currently trading
* Proof Type
* Total Coins Mined
* Total Coin Supply

Some of these components are non-numerical, and among the 1253 entries are some null fields, therefore the preprocessing to create a dataset that can be used with the unsupervised algorithm is the following:

1. Filter out the cryptocurrencies that are not currently traded and dropping that columns after it has been used.
2. Dropping all entries will null values
3. Removing all entries with a Tocal Coins Mined value that's equal to 0
4. Removing the Coin Name attribute since it's not relevant to our grouping algorithm
5. Create dummies from the algorithm and proof type attributes.

The resulting dataset, with 523 entries, is then scaled using SKLearn Standard Scaler and reduced from 98 components to 3 using Principal Component Analysis.

In order to find the optimal number of clusters for the KMeans model, an elbow curve is created using the inertia from the KMeans model. Then, the KMmeans model is created with a cluster number of 4 and then predicts the group in which each cryptocurrency falls in.

![Resulting_Table](/Images/hvplot_table.jpeg)

## Results

![3D_PC_Scatter_Plot](/Images/newplot.png)

The first result is this 3D plot which uses the Principal Components 1, 2 and 3 as the x,y,z coordinates. When hovering over a point, this graph shows the Coin Name, Principal Components and its Algorithm. 

All the entries in the dataset had a label assigned from the KMeans model prediction, and according to said label is the color and shape that's assigned to each datapoint.

![2D_Coin_Mined_Supply_Plot](/Images/bokeh_plot.png)

An additional plot is created by grabbing and scaling only the TotalCoinsMined and TotalCoinSupply attributes from all entries. These 2 valus are used as the x and y coordinates for the 2D scatter plot.