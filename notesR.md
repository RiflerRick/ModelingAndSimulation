## Notes on R

Follow the tutorial of R on codeSchool in order for a hands on experience for R

### Matrices:
#### Matrices Introduction

For making a matrix 3 rows high, 4 columns wide, all its fields set to 0 use the following command

`matrix(0,3,4)`

Now lets actually fill that matrix with a few values

`a<-1:12`

This above line creates a vector

`print(a)`

This prints the values of a all in a single line

Now the magic happens when you use the vector a to actually initialize the elements of the matrix defined by 
the matrix function

`matrix(a,3,4)`

We can also reshape the vector itself into a matrix in the following way

`plank<-1:8` 
`dim(plank)<-c(2,4)`

what the above line does is that it reshapes the vector plank into a matrix of dimensions 2*4

The dim function is used to set the dimensions of a matrix (essentially reshaping the matrix)

The function `matrix()` works in the following way:
- the first arguement specifies the elements of the matrix. If its a single value then that single value populates the matrix, if it is a vector the vector populates the matrix
- the second arguement specifies the rows
- the third arguement specifies the columns

#### Matrix access:

Matrices can be accessed using the same way like a normal vector

For example:
`plank[2,3]`

In a similar manner just like vectors we can assign elements inside the matrix. For example:

`plank[2,3]<-0`

We can get an entire row in the following manner:

`plank[2,]`

We can get the columns in the following manner

We can provide ranges of values for columns in the following manner:

`plank[,2:4]`

#### Matrix Plotting:

This is actually pretty interesting and quite unique actually
Text output is useful when the matrices are small, but when it comes to large and complicated matrices text visualizations do not suffice and we need to create more vivid and graphic visualizations.

So lets say we need an elevation map of a sandy beach

Its flat, everything is one meter above the sea level, so we do the following

`elevation<-matrix(1,10,10)`

Now imagine we dug down the sea level at a point to find a treasure chest, so we set the element at 4,6 to 0

`elevation[4,6]<-0`

We can now plot a contour map of the matrix using the following command

`contour(elevation)`

Better still its possible to create a 3d perspective plot using the following function:

`persp(elevation)`

The function persp() works in such a way that by default, your top is set to the highest value in the matrix, 1 in this case, however that can be changed

`persp(elevation,expand=0.2)`

this expand parameter is used for the purpose of expanding only upto a specified limit

Similarly there is a function called image() that creates heat map of the matrix, cool right???

`image(volcano)`, try this to see what happens

### Summary Statistics:

Simply throwing some data in the face of the audience will only confuse them, our job should be to explain that data to the audience, R has some tools to do that, lets check those out.

#### Mean

Examples will help explain the concept even more thoroughly. 

Example:

Determining the health of crew members of a ship is necessary. Below is a vector of all the crew members along with their remaining limbs.

mind u that the names function is used for the purpose of creating keys of values just like in a python dictionary.

`limbs<-c(4,3,4,3,2,4,4,4,)`
`names(limbs)<-c('one-eye','peg-leg','simtty','Hook','Scooter','Dan','Mikey','BlackBeard')`

One easy way of assessing the battle-readiness is to check the Mean

`mean(limbs)`

This function computes the mean and returns it

Lets now actually see the barplot of the values

`barplot(limbs)`

If we wanna compare the values in the barplot with the average value, we may wanna do that. In that case we can use the abline() function that takes an h parameter at which to draw a horizontal line and a v parameter to draw a vertical line.

`abline(h=mean(limbs))`

The function edits the previous graph.

#### Median

Now that we have mean, lets try Median
Lets say we get a crew member that completely skews the mean.

For example we get a data just like the previous one with the limbs except that here we have a last crew member that was added with a value of 14 limbs. The average in such a case will come out to be 4.7 limbs which is misleading.

In these cases we use the median. The data is sorted and then the middle value is taken, if there are 2 middle values, they are averaged.

The function as u have already guessed, is :

`median(limbs)`

#### Standard Deviation

Standard Deviation is typically used to describe the range of typical values for a data set. For a group of numbers it shows how much they vary from the average value.

How its calculated is not important as R provides a function to do exactly that

`deviation<-sd(pounds)`

### Factors:

Often we wanna group data by category of some sort:
R uses the factor function in order to do just that.

Imagine we have an vector of the following form:

`chests <- c('gold', 'silver', 'gems', 'gold', 'gems')`

Now if we use the function factor() on it, in that case the vector will be factored based on the repeating elements.

`types<-factor(chests)`

this will create a new array types that has factor levels of the vector chests

so basically,

`print(types)`
`[1] gold   silver gems   gold   gems  `
`Levels: gems gold silver`

Notice that Levels is not having any double quotes around it, thats because they are not numbers they are essentially, integer references to the factor levels:

`levels(types)`
`[1] "gems"   "gold"   "silver"`

These are the levels.

#### Plotting with the help of factors:

Now sometimes plotting can be a real necessity when plotting with factors and so lets see how that works.
Lets say we have the following vectors.

` weights <- c(300, 200, 100, 250, 150)`
` prices <- c(9000, 5000, 12000, 7500, 18000)`
` plot(weights, prices)`

So this will plot the functions in such a manner that a point is at (300,9000) and so on.

#### Plot Characters(pch)

So we can use plot characters using the pch parameter which takes in integer values as a vector and accordingly assign different points as a special character.

`plot(weights,prices,pch=as.integer(types))`

This types refers to the vector factor(chests)

We can do legends in the following way:

`legend("topright",c("gems","gold","silver"),pch=1:3)`

formal parameters are pretty self explainatory

Here is a better version of legend such that we do not need to change the legend because of the change of the chest

 `legend("topright",levels(types),pch=1:length(levels(types)))`

### Data Frames:

Data Frames are something like database tables in that they store data in the form of tables(rows and columns)

Its rather easy to actually use a dataframe.

`treasure <- data.frame(weights, prices, types)`

Now if we print treasure we will find the data arranged in the form of tables.

#### Accessing Data Frames:

Accessing data frames is rather simple.

`treasure[[2]]`

Basically the syntax is name of the data frame[[column number]] or column name also works.

For a quicker access, we get name of the dataframe$column name

For example:

`treasure$weights`

#### Loading Data Frames:

We can use a csv file for loading a data frame, in the following manner.

`read.csv("targets.csv")`

provided targets.csv actually exists in the same folder.

Now for loading files that use separator characters other than commas we can use the following function in the following manner.

`read.table("infantry.txt",sep="\t")`

for a tab separation.

Now the first line in the text file may actually be the file header. 
 







