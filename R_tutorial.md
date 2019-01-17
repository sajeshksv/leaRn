leaRn
================

Session 1: Introduction to R
============================

Vectors
-------

A form of reading and storing data (strings, integers, etc.) in R. The `<-` is called an assignment operator. This means that the operator assigns a value on the right hand side to the variable which we have named in the left hand side. Although both `=` and `<-` can be used for assigning operations, the latter gives a more visual representation of the direction in which the operation occurs. Using `#` in the script will comment out that portion, which makes R to skip that line of code

``` r
myFirstVector <- c("Kavya", "Sraman", "Bahee", "Shweta", "Anna", "Krishanu", "Amamah", "Geervani", "Sajesh")

myFirstVector       # gives the output of the variable, whose value(s) is displayed in the console.
```

    ## [1] "Kavya"    "Sraman"   "Bahee"    "Shweta"   "Anna"     "Krishanu"
    ## [7] "Amamah"   "Geervani" "Sajesh"

The `[ ]` in the beginning of each line shows the element number (index). In the above output, we can easily see there are 9 elements, with *Kavya* being the first element and *Sajesh* being the ninth element. A few things to keep in mind when creating variable names are outlined in the code below

``` r
myFirstVector <- c(Kavya)        # is wrong because Kavya is not within double quotations.
```

    ## Error in eval(expr, envir, enclos): object 'Kavya' not found

``` r
my First Vector <- c("Kavya")        # has space in variable name; hence wrong
```

    ## Error: <text>:1:4: unexpected symbol
    ## 1: my First
    ##        ^

``` r
1stvector <- c("Kavya")        # starts with a number
```

    ## Error: <text>:1:2: unexpected symbol
    ## 1: 1stvector
    ##      ^

``` r
vector1 <- c("Kavya")        # has no error since the number does not come in the beginning
```

We can easily update existing data, by adding new elements to it. In the next step, we create a new vector named `RParticipants` using the data from `myFirstVector` and update it with one more entry.

``` r
RParticipants <- c(myFirstVector, "Tarun")
```

Let us create a new vector with the age of each individual from `RParticipants`. In case we want to find the length of the vector, we use the function `length`. If we want to find the average age of the group, we can simply run `mean` on the vector. The ouput panel shows that our vector has 10 entries and the mean age of the group is 24.8.

``` r
RBatch <- c(25,23,24,25,23,26,27,25,24,26)
length(RBatch)
```

    ## [1] 10

``` r
mean(RBatch)
```

    ## [1] 24.8

Data frames
-----------

Dataframes are two-deimensional arrangement of data where each column is a variable, and each row usually consists one entry of the collected data. Let us try and generate a dataframe from the two vectors we had created earlier. For this, we use the `data.frame` function. Once we create the dataframe, we check the contents of the dataframe by calling it using the variable name.

``` r
RGroup <- data.frame(RParticipants, RBatch)
RGroup
```

    ##    RParticipants RBatch
    ## 1          Kavya     25
    ## 2         Sraman     23
    ## 3          Bahee     24
    ## 4         Shweta     25
    ## 5           Anna     23
    ## 6       Krishanu     26
    ## 7         Amamah     27
    ## 8       Geervani     25
    ## 9         Sajesh     24
    ## 10         Tarun     26

### Slicing and dicing dataframes

Despite my best efforts to stay young, the nature of time forces me to get older with each passing day, and this fact makes it imperative for me to update my age in the data frame. This process is going to introduce us to a few new functions to subset and update dataframes.

Subsetting of a dataframe is done using sqaure brackets. `myDummy[2,3]` would return the value of the second row, third column of your `myDummy` dataframe. We can see that `Sajesh` is the ninth entry in `RGroup`, so to change the age associated with `Sajesh`, we run the following command

``` r
RGroup[9,2] <- 25
RGroup
```

    ##    RParticipants RBatch
    ## 1          Kavya     25
    ## 2         Sraman     23
    ## 3          Bahee     24
    ## 4         Shweta     25
    ## 5           Anna     23
    ## 6       Krishanu     26
    ## 7         Amamah     27
    ## 8       Geervani     25
    ## 9         Sajesh     25
    ## 10         Tarun     26

With the above command, we have instructed R to seek out the **ninth row** and **second column** and assign to it a value of 25.

A much better way of doing this, especially when you want to edit larger datasets, is to use conditional statements. Conditional statements are Boolean in nature i.e. they validate if the statement we have entered is true or false. Examples (and corresponding outputs) of commonly used statements are below:

``` r
"a" == "a" # claims that the alphabet a is the same as the alphabet a
```

    ## [1] TRUE

``` r
"a" == "b" # claims that the alphabet a is the same as the alphabet b
```

    ## [1] FALSE

``` r
"a" > "b"  # claims that the alphabet a is greater than alphabet b
```

    ## [1] FALSE

``` r
27 >= 26   # The integer 27 is greater than or equal to 26
```

    ## [1] TRUE

``` r
154 <= 207 # The integer 154 is lesser than or equal to 207
```

    ## [1] TRUE

``` r
18 != 18   # The integer 18 is not equal to the integer 18
```

    ## [1] FALSE

To edit another entry in `RGroup`, we use a conditional statement. To edit Kavya's age in the dataframe, we run the following command.

``` r
RGroup$RBatch[RGroup$RParticipants == "Kavya"] <- 24
RGroup
```

    ##    RParticipants RBatch
    ## 1          Kavya     24
    ## 2         Sraman     23
    ## 3          Bahee     24
    ## 4         Shweta     25
    ## 5           Anna     23
    ## 6       Krishanu     26
    ## 7         Amamah     27
    ## 8       Geervani     25
    ## 9         Sajesh     25
    ## 10         Tarun     26

You would notice that we have used a new symbol in this step. It is `$` which is used to choose a specific variable in the dataframe. The above command is instructing `R` to do the following: in the row in `RGroup` whose value for the variable `RParticipant` is `Kavya`, change the value of the variable `RBatch` to 24.

In case we want to add a new entry into the dataframe, it can be done by creating a new vector corresponding to the entry and using a function called `rbind` (row-bind).

``` r
newMember <- c("Bruce", 59)
RGroup <- rbind(RGroup, newMember)
```

    ## Warning in `[<-.factor`(`*tmp*`, ri, value = "Bruce"): invalid factor
    ## level, NA generated

``` r
RGroup
```

    ##    RParticipants RBatch
    ## 1          Kavya     24
    ## 2         Sraman     23
    ## 3          Bahee     24
    ## 4         Shweta     25
    ## 5           Anna     23
    ## 6       Krishanu     26
    ## 7         Amamah     27
    ## 8       Geervani     25
    ## 9         Sajesh     25
    ## 10         Tarun     26
    ## 11          <NA>     59

We notice that an error pops up, showing that we have tried inputting an invalid factor level. If we check the dataframe, we notice that the `RParticipants` variable is shown as `<fctr>`. This means that we need to either input the term "Bruce" as a factor, or change the variable type of the `RParticipants` column. We will do the latter in this case.

``` r
RGroup$RParticipants <- as.character(RGroup$RParticipants)
RGroup <- rbind(RGroup, newMember)
RGroup
```

    ##    RParticipants RBatch
    ## 1          Kavya     24
    ## 2         Sraman     23
    ## 3          Bahee     24
    ## 4         Shweta     25
    ## 5           Anna     23
    ## 6       Krishanu     26
    ## 7         Amamah     27
    ## 8       Geervani     25
    ## 9         Sajesh     25
    ## 10         Tarun     26
    ## 11          <NA>     59
    ## 12         Bruce     59

Since the 11th row is to be removed, due to the earlier factor-character issue, we do so as below.

``` r
RGroup <- RGroup[-11,]
RGroup
```

    ##    RParticipants RBatch
    ## 1          Kavya     24
    ## 2         Sraman     23
    ## 3          Bahee     24
    ## 4         Shweta     25
    ## 5           Anna     23
    ## 6       Krishanu     26
    ## 7         Amamah     27
    ## 8       Geervani     25
    ## 9         Sajesh     25
    ## 10         Tarun     26
    ## 12         Bruce     59

Repetition using `for` loop
---------------------------

A frequent portion of any function you create would be to do a task repeatedly. Loops are instructions which a program uses to do a recurring task. Let us understand how to create a loop to do a lengthy, repetitive calculation. We use a `for` loop for this task. A for loop is structured as

``` r
for (# CONDITION) {
  # TASK
}
```

### Calculating the product of all odd numbers between 1 and 100

A basic loop below calculates the product of all numbers from 1 to 100. Prior to running the code, we need to establish the starting value of the output variable, and our desired values are iterated into this variable.

``` r
oddProduct <- 1    # setting the initial value of the output variable 
for(i in 1:100){
  oddProduct <- oddProduct*i
  print(oddProduct)
}
```

    ## [1] 1
    ## [1] 2
    ## [1] 6
    ## [1] 24
    ## [1] 120
    ## [1] 720
    ## [1] 5040
    ## [1] 40320
    ## [1] 362880
    ## [1] 3628800
    ## [1] 39916800
    ## [1] 479001600
    ## [1] 6227020800
    ## [1] 87178291200
    ## [1] 1.307674e+12
    ## [1] 2.092279e+13
    ## [1] 3.556874e+14
    ## [1] 6.402374e+15
    ## [1] 1.216451e+17
    ## [1] 2.432902e+18
    ## [1] 5.109094e+19
    ## [1] 1.124001e+21
    ## [1] 2.585202e+22
    ## [1] 6.204484e+23
    ## [1] 1.551121e+25
    ## [1] 4.032915e+26
    ## [1] 1.088887e+28
    ## [1] 3.048883e+29
    ## [1] 8.841762e+30
    ## [1] 2.652529e+32
    ## [1] 8.222839e+33
    ## [1] 2.631308e+35
    ## [1] 8.683318e+36
    ## [1] 2.952328e+38
    ## [1] 1.033315e+40
    ## [1] 3.719933e+41
    ## [1] 1.376375e+43
    ## [1] 5.230226e+44
    ## [1] 2.039788e+46
    ## [1] 8.159153e+47
    ## [1] 3.345253e+49
    ## [1] 1.405006e+51
    ## [1] 6.041526e+52
    ## [1] 2.658272e+54
    ## [1] 1.196222e+56
    ## [1] 5.502622e+57
    ## [1] 2.586232e+59
    ## [1] 1.241392e+61
    ## [1] 6.082819e+62
    ## [1] 3.041409e+64
    ## [1] 1.551119e+66
    ## [1] 8.065818e+67
    ## [1] 4.274883e+69
    ## [1] 2.308437e+71
    ## [1] 1.26964e+73
    ## [1] 7.109986e+74
    ## [1] 4.052692e+76
    ## [1] 2.350561e+78
    ## [1] 1.386831e+80
    ## [1] 8.320987e+81
    ## [1] 5.075802e+83
    ## [1] 3.146997e+85
    ## [1] 1.982608e+87
    ## [1] 1.268869e+89
    ## [1] 8.247651e+90
    ## [1] 5.443449e+92
    ## [1] 3.647111e+94
    ## [1] 2.480036e+96
    ## [1] 1.711225e+98
    ## [1] 1.197857e+100
    ## [1] 8.504786e+101
    ## [1] 6.123446e+103
    ## [1] 4.470115e+105
    ## [1] 3.307885e+107
    ## [1] 2.480914e+109
    ## [1] 1.885495e+111
    ## [1] 1.451831e+113
    ## [1] 1.132428e+115
    ## [1] 8.946182e+116
    ## [1] 7.156946e+118
    ## [1] 5.797126e+120
    ## [1] 4.753643e+122
    ## [1] 3.945524e+124
    ## [1] 3.31424e+126
    ## [1] 2.817104e+128
    ## [1] 2.42271e+130
    ## [1] 2.107757e+132
    ## [1] 1.854826e+134
    ## [1] 1.650796e+136
    ## [1] 1.485716e+138
    ## [1] 1.352002e+140
    ## [1] 1.243841e+142
    ## [1] 1.156773e+144
    ## [1] 1.087366e+146
    ## [1] 1.032998e+148
    ## [1] 9.916779e+149
    ## [1] 9.619276e+151
    ## [1] 9.42689e+153
    ## [1] 9.332622e+155
    ## [1] 9.332622e+157

This function instructs `R` to take each number from 1 to 100, and multiply it to the value of oddProduct. In the first round of iteration, value of `oddProduct` is 1 and at the end of the loop, that value is updated to 2, which is printed from the `print` function. In the second iteration, the value of `oddProduct` is 2. This proceeds in this repetetive manner until i reaches 100.

Our aim is to have a loop for all odd numbers in the above range. For this we use an `if-else` statement, whose structure is as below:

``` r
for (# CONDITIONAL STATEMENT) {
  # TASK
}
```

In the last section on dataframes, we had discussed conditional statements as well. Here, the condition is `odd numbers between 1 and 100`. For this truth statement, we use the `modulo operator %%`. You can read more about modulo operators [here](https://en.wikipedia.org/wiki/Modulo_operation). Our final loop will be as below. Once the loop is run, we call the final value of `oddProduct` with the `print` call. This ensures that a lengthy output is not generated.

``` r
oddProduct <- 1
for (i in 1:100){
  if (i %% 2 == 1){
    oddProduct <- oddProduct*i
  }
}
print(oddProduct)
```

    ## [1] 2.725392e+78

When R encounters this code, it first takes the `i = 1`, and run the Boolean statement on 1, which gives the following output, which instructs R to proceed to the next line in the loop, which is to update the value of `oddProduct`.

    ## [1] TRUE

In the next iteration (`i = 2`) when R runs the code and at the Boolean statement stage, the output would be as below, thus instructing R to skip the remaining portion of the code and restart with `i = 3`

    ## [1] FALSE

------------------------------------------------------------------------

Session 2: Functions - The Beginning
====================================

#### Prerequisites

-   Subsetting dataframe
-   Writing loops

Functions
---------

-   **Task: load a file, calculate the duration of each [waggle dance](https://www.youtube.com/watch?v=-7ijI-g4jHg) for each honey bee in a 5-minute obervation, and output the summary statistics (mean and standard deviation) into a dataframe**

A good starting point when creating a code is to visualise what the final product you want is. In our case, we need it to look like the output below, and it provides us a destination to which the function should shape to.

    ##    trialID subjectName waggle_mean waggle_sd
    ## 1 dummy123         001        3.56      0.02

In the dataset to be analysed, each waggle dance is marked by the start time and end time, which are not explicitly stated in the file. In case of a subset of the data for one subject, the odd rows would correspond to starts of the waggle dances and the even rows would correspond to the ends of the waggle dances. Hence the vector containing the durations of all the waggle dances for a subject can be obtained by subtracting the vector of the start times from the vector of the end times. The mean and standard deviations of dances for each bee can be calculated from this vector.

### Part 1: Read CSV file

A very popular format for storing datasets is as comma seperated value (CSV) sheets. For the purpose of this demo, I am going to use a small CSV file shared with you all. I load the CSV file into the R environment using `read.csv` function. We create an empty output dataframe `waggleFinal` similar to the final dataframe we want. The data will be stored after each iteration in `waggleFinal`.

``` r
x = "data_in/20181215_00934.csv"
sampleData <- read.csv(x)

sampleData    # returns the whole dataframe
```

    ##    Time
    ## 1  0.08
    ## 2  0.24
    ## 3 10.20
    ## 4 14.16
    ## 5 20.08
    ## 6 27.96
    ##                                                         Media.file.path
    ## 1 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 2 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 3 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 4 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 5 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 6 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ##   Total.length FPS Subject Behavior Comment Status     X
    ## 1       332.29  25       2        w      NA     NA POINT
    ## 2       332.29  25       1        w      NA     NA POINT
    ## 3       332.29  25       1        w      NA     NA POINT
    ## 4       332.29  25       2        w      NA     NA POINT
    ## 5       332.29  25       3        w      NA     NA POINT
    ## 6       332.29  25       3        w      NA     NA POINT

``` r
head(sampleData)    # returns the first 5 rows of the dataframe
```

    ##    Time
    ## 1  0.08
    ## 2  0.24
    ## 3 10.20
    ## 4 14.16
    ## 5 20.08
    ## 6 27.96
    ##                                                         Media.file.path
    ## 1 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 2 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 3 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 4 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 5 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ## 6 C:/Users/Administrator/Desktop/iiser-tvm/IISER_BSB/20181215/00934.MTS
    ##   Total.length FPS Subject Behavior Comment Status     X
    ## 1       332.29  25       2        w      NA     NA POINT
    ## 2       332.29  25       1        w      NA     NA POINT
    ## 3       332.29  25       1        w      NA     NA POINT
    ## 4       332.29  25       2        w      NA     NA POINT
    ## 5       332.29  25       3        w      NA     NA POINT
    ## 6       332.29  25       3        w      NA     NA POINT

``` r
waggleFinal <- data.frame(trialID = NA, subjectName = NA, waggle_mean = NA, waggle_sd = NA)
```

### Part 2: Loop for extracting the data subject-wise

Before we write our function to obtain data from multiple files, we will establish the general layout using one file, and then migrate these steps into our function code. For any file that we run, the `trialID` will remain constant for all subjects. We create a variable outside the loop named `trialName`. This variable will be populated by the file name when the function is run eventually (more on that later).

``` r
trialName <- as.character(x)
```

The next step is to create the loop which will calculate the mean and the standard deviation for the dances of each bee. In the file that we are using, the number of subjects is only three. So the range in the loop can be given as `for (i in 1:3)...`. What if there are 20 subjects in another file? What if you have to calculate activiities across 200 flies? We use the `unique` function for this purpose. You would notice that the order of subjects is 2, 1 and 3. This is not a case of concern for us since we will be calling the subjects using `for (i in 1:numSubjects)`.

``` r
uniqueSubjects <- unique(sampleData$Subject)
numSubjects <- length(uniqueSubjects)
numSubjects
```

    ## [1] 3

``` r
for (i in 1:numSubjects){
  trialID <- trialName
  
  sub_name <- i
  # subsetting the data based on subject i
  subsetData <- sampleData[sampleData$Subject == i,]    
  
  # the rownames in subsetData from the previous step are the same as the ones in sampleData. Since we want new rownames for our subsetted data, starting from rowname = 1, we use the rownames() statement, and instruct R to set the rownames starting 1 to how much ever rows the subsetData has, which is obtained by nrow()
  rownames(subsetData) <- c(1:nrow(subsetData))
  
  # the odd rows are extracted from subsetData and the time variable of this dataset is stored in startTimes vector. The same is carried out for endTimes. 
  oddRows <- subsetData[as.numeric(rownames(subsetData)) %% 2 == 1,]
  startTimes <- oddRows$Time
  
  evenRows <- subsetData[as.numeric(rownames(subsetData)) %% 2 == 0,]
  endTimes <- evenRows$Time
  
  # the duration vector for the bee is calculated by subtracting startTimes from endTimes
  waggleDuration <- endTimes - startTimes
  
  # mean and standard deviation across all dances for bee i are calculated using mean() and sd() functions
  meanWaggles <- mean(waggleDuration)
  sdWaggles <- sd(waggleDuration)
  
  # the different parts of the output of this loop are collated into one vector which will be added to the waggleFinal dataset using rbind()
  newEntry <- c(trialID, sub_name, meanWaggles, sdWaggles)
  
  waggleFinal <- rbind(waggleFinal, newEntry)
    
}

# the first row of waggleFinal is still comprised of NA values which we added as placeholders when creating the variable. We remove that after the loop is run.

waggleFinal <- waggleFinal[-1,] # removes the first row of the dataframe

waggleFinal
```

    ##                      trialID subjectName waggle_mean waggle_sd
    ## 2 data_in/20181215_00934.csv           1        9.96      <NA>
    ## 3 data_in/20181215_00934.csv           2       14.08      <NA>
    ## 4 data_in/20181215_00934.csv           3        7.88      <NA>

Session 3: Functions - The Conclusion
=====================================

### Part 3: The function

So far, we have written a code, that given a file, will extract and collate summary statistics for each individual bee. We need to wrap this into a function so that our job (extract data from a set of files) become much, much easier. This final step is quite short, and adds only a few more lines to our code. We create function in R using the `function` function (duh!). If you remember from our last session, the only changing entity we used was the file name. The remaining portions of our code will do the same thing over and over again once the file name is provided. Hence, the only parameter we need to define in our function is the file name. Such parameters of a function are called arguments. We define a function named `waggleSummary` with one parameter, `x`. The body of the function will be the code you had written in Session 2.

``` r
waggleSummary = function(x){
  
  # load the dataframe into memory
  sampleData <- read.csv(x)
  
  # create empty dataframe to store the output data
  waggleFinal <- data.frame(trialID = NA, 
                            subjectName = NA, 
                            waggle_mean = NA, 
                            waggle_sd = NA)
  
  # store the trial name
  trialName <- as.character(x)
  
  # obtain number of individuals for the loop to iterate over
  uniqueSubjects <- unique(sampleData$Subject)
  numSubjects <- length(uniqueSubjects)
  
  # define the loop
  for (i in 1:numSubjects){
  trialID <- trialName
  
  sub_name <- i
  
  # subsetting the data based on subject i
  subsetData <- sampleData[sampleData$Subject == i,]    
  
  # reset the rownames
  rownames(subsetData) <- c(1:nrow(subsetData))
  
  # extract start and end times of waggle dances 
  oddRows <- subsetData[as.numeric(rownames(subsetData)) %% 2 == 1,]
  startTimes <- oddRows$Time
  
  evenRows <- subsetData[as.numeric(rownames(subsetData)) %% 2 == 0,]
  endTimes <- evenRows$Time
  
  # the following series of steps need to be done IF AND ONLY IF the number of start   
  # time entries and the number of end time entries are equal. Hence, we introduce a 
  # check in place, instructing R to skip this iteration of the for loop when this  
  # equality condition is not satisfied.
    
  if(length(startTimes) != length(endTimes)){
    next
    }
  
  # make a subset table with the times
  timeTable <- data.frame(startTimes, endTimes)
  
  # the duration vector for the bee is calculated by subtracting startTimes from endTimes
  waggleDuration <- timeTable$endTimes - timeTable$startTimes
  
  # calculate mean and standard deviation of the durations
  meanWaggles <- mean(waggleDuration)
  sdWaggles <- sd(waggleDuration)
  
  # create new vector entry
  newEntry <- c(trialID, sub_name, meanWaggles, sdWaggles)
  
  # send output to empty dataframe
  waggleFinal <- rbind(waggleFinal, newEntry)
  }
  
  waggleFinal <- waggleFinal[-1,] # removes the first row (with NAs) of the dataframe

  
  return(waggleFinal)
}
```

Once the code is complete, we load it into the R environment by running the code. You can test if your function is working as expected by giving the dataset we used yesterday as the argument.

``` r
waggleSummary("data_in/20181215_00934.csv")
```

    ##                      trialID subjectName waggle_mean waggle_sd
    ## 2 data_in/20181215_00934.csv           1        9.96      <NA>
    ## 3 data_in/20181215_00934.csv           2       14.08      <NA>
    ## 4 data_in/20181215_00934.csv           3        7.88      <NA>

We have just successfully made our first function!!! This still requires us to run each file separately. To overcome this obstacle, we use three more lines of code to cycle through all the files in a directory and provide the final dataset we require. The first of it (`list,files()`) creates a vector with the list of the files in the parent directory. `lapply` applies our function `waggleSummary` to all elements in the vector, and stores the output as a list of dataframes. The last line binds each dataframe row-wise and creates the final output.

``` r
files = list.files(path = "data_in/", pattern = "*.csv", full.names = T)
results = lapply(files, waggleSummary)
waggle_out = as.data.frame(do.call(rbind, results))
waggle_out
```

    ##                        trialID subjectName      waggle_mean
    ## 2  data_in//20181215_00934.csv           1             9.96
    ## 3  data_in//20181215_00934.csv           2            14.08
    ## 4  data_in//20181215_00934.csv           3             7.88
    ## 21 data_in//20181215_00935.csv           1             5.88
    ## 31 data_in//20181215_00935.csv           2            18.84
    ## 41 data_in//20181215_00935.csv           3            18.22
    ## 5  data_in//20181215_00935.csv           4 7.95999999999999
    ## 22 data_in//20181215_00937.csv           1            18.16
    ## 32 data_in//20181215_00937.csv           2             23.2
    ## 42 data_in//20181215_00937.csv           4            14.52
    ## 51 data_in//20181215_00937.csv           5            23.84
    ## 6  data_in//20181215_00937.csv           7            30.24
    ## 23 data_in//20181217_00938.csv           1            14.64
    ## 33 data_in//20181217_00938.csv           2             20.2
    ## 43 data_in//20181217_00938.csv           3            15.24
    ## 52 data_in//20181217_00938.csv           4            14.56
    ## 61 data_in//20181217_00938.csv           5               26
    ## 7  data_in//20181217_00938.csv           6             28.2
    ## 8  data_in//20181217_00938.csv           7            22.44
    ## 9  data_in//20181217_00938.csv           8             10.6
    ## 10 data_in//20181217_00938.csv           9             17.6
    ## 11 data_in//20181217_00938.csv          10            10.84
    ## 12 data_in//20181217_00938.csv          11 5.60000000000001
    ## 13 data_in//20181217_00938.csv          12            14.04
    ## 14 data_in//20181217_00938.csv          13               65
    ## 24 data_in//20181217_00940.csv           2            27.04
    ## 34 data_in//20181217_00940.csv           3            23.36
    ## 44 data_in//20181217_00940.csv           5             26.6
    ## 53 data_in//20181217_00940.csv           6 9.60000000000002
    ## 62 data_in//20181217_00940.csv           7            10.96
    ## 71 data_in//20181217_00940.csv           8             11.6
    ## 25 data_in//20181217_00941.csv           1            17.52
    ## 35 data_in//20181217_00941.csv           2             39.6
    ## 45 data_in//20181217_00941.csv           3            14.72
    ## 54 data_in//20181217_00941.csv           4            25.12
    ## 63 data_in//20181217_00941.csv           5            25.84
    ## 72 data_in//20181217_00941.csv           6             20.8
    ## 81 data_in//20181217_00941.csv           7            24.72
    ## 26 data_in//20181217_00942.csv           1            17.68
    ## 36 data_in//20181217_00942.csv           2            19.92
    ## 46 data_in//20181217_00942.csv           3            14.48
    ## 55 data_in//20181217_00942.csv           4            17.52
    ## 64 data_in//20181217_00942.csv           5            19.68
    ##           waggle_sd
    ## 2              <NA>
    ## 3              <NA>
    ## 4              <NA>
    ## 21             <NA>
    ## 31             <NA>
    ## 41 2.29102597104439
    ## 5  5.14773736703807
    ## 22             <NA>
    ## 32             <NA>
    ## 42 2.20617315730203
    ## 51             <NA>
    ## 6              <NA>
    ## 23             <NA>
    ## 33             <NA>
    ## 43             <NA>
    ## 52             <NA>
    ## 61             <NA>
    ## 7              <NA>
    ## 8              <NA>
    ## 9              <NA>
    ## 10             <NA>
    ## 11             <NA>
    ## 12             <NA>
    ## 13             <NA>
    ## 14             <NA>
    ## 24             <NA>
    ## 34             <NA>
    ## 44             <NA>
    ## 53             <NA>
    ## 62             <NA>
    ## 71             <NA>
    ## 25             <NA>
    ## 35             <NA>
    ## 45             <NA>
    ## 54             <NA>
    ## 63             <NA>
    ## 72             <NA>
    ## 81             <NA>
    ## 26             <NA>
    ## 36             <NA>
    ## 46             <NA>
    ## 55             <NA>
    ## 64             <NA>
