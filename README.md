# Assignment-24.1
Perform the below given activities:
a. Take a sample data set of your choice
b. Apply random forest, logistic regression using Spark R
c. Predict for new dataset

ANSWER:
> library(ISLR)
> attach(Carseats)
> Carseats=Carseats1[-1]
Error: object 'Carseats1' not found
> dim(Carseats)
[1] 400  11
> #Sales is continous data
> #if saless<=8 then No, else Yes
> #new variable High, high already contains sales
> High<- ifelse(Carseats$Sales<=8, 'No','Yes')
> Sales is continous data
Error: unexpected symbol in "Sales is"
> #if saless<=8 then No, else Yes
> #new variable High, high already contains sales
> High<- ifelse(Carseats$Sales<=8, 'No','Yes')
> dim(Carseats)
[1] 400  11
> str(High)
 chr [1:400] "Yes" "Yes" "Yes" "No" "No" "Yes" "No" "Yes" "No" "No" "Yes" ...
> #include High in data Carseats
> Carseats<-data.frame(Carseats, High)
> dim(Carseats)
[1] 400  12
> names(Carseats)
 [1] "Sales"       "CompPrice"   "Income"      "Advertising" "Population" 
 [6] "Price"       "ShelveLoc"   "Age"         "Education"   "Urban"      
[11] "US"          "High"       
> #building Tree
> library(tree)
> tree.carseats<-tree(High~.-Sales,Carseats)
> summary(tree.carseats)

Classification tree:
tree(formula = High ~ . - Sales, data = Carseats)
Variables actually used in tree construction:
[1] "ShelveLoc"   "Price"       "Income"      "CompPrice"   "Population" 
[6] "Advertising" "Age"         "US"         
Number of terminal nodes:  27 
Residual mean deviance:  0.4575 = 170.7 / 373 
Misclassification error rate: 0.09 = 36 / 400 
> #removed Sales as predictor from whole dataset
> #smaller the RMSE better, Residual Mean Deviance
> #Out of 400 only 36 cases 
> #where misclassified, so 91% accurancy (whole data, because only 400 cases taken)
> #plot the tree
> plot(tree.carseats)
> text(tree.carseats, pretty=0)
> tree.carseats
node), split, n, deviance, yval, (yprob)
      * denotes terminal node

  1) root 400 541.500 No ( 0.59000 0.41000 )  
    2) ShelveLoc: Bad,Medium 315 390.600 No ( 0.68889 0.31111 )  
      4) Price < 92.5 46  56.530 Yes ( 0.30435 0.69565 )  
        8) Income < 57 10  12.220 No ( 0.70000 0.30000 )  
         16) CompPrice < 110.5 5   0.000 No ( 1.00000 0.00000 ) *
         17) CompPrice > 110.5 5   6.730 Yes ( 0.40000 0.60000 ) *
        9) Income > 57 36  35.470 Yes ( 0.19444 0.80556 )  
         18) Population < 207.5 16  21.170 Yes ( 0.37500 0.62500 ) *
         19) Population > 207.5 20   7.941 Yes ( 0.05000 0.95000 ) *
      5) Price > 92.5 269 299.800 No ( 0.75465 0.24535 )  
       10) Advertising < 13.5 224 213.200 No ( 0.81696 0.18304 )  
         20) CompPrice < 124.5 96  44.890 No ( 0.93750 0.06250 )  
           40) Price < 106.5 38  33.150 No ( 0.84211 0.15789 )  
             80) Population < 177 12  16.300 No ( 0.58333 0.41667 )  
              160) Income < 60.5 6   0.000 No ( 1.00000 0.00000 ) *
              161) Income > 60.5 6   5.407 Yes ( 0.16667 0.83333 ) *
             81) Population > 177 26   8.477 No ( 0.96154 0.03846 ) *
           41) Price > 106.5 58   0.000 No ( 1.00000 0.00000 ) *
         21) CompPrice > 124.5 128 150.200 No ( 0.72656 0.27344 )  
           42) Price < 122.5 51  70.680 Yes ( 0.49020 0.50980 )  
             84) ShelveLoc: Bad 11   6.702 No ( 0.90909 0.09091 ) *
             85) ShelveLoc: Medium 40  52.930 Yes ( 0.37500 0.62500 )  
              170) Price < 109.5 16   7.481 Yes ( 0.06250 0.93750 ) *
              171) Price > 109.5 24  32.600 No ( 0.58333 0.41667 )  
                342) Age < 49.5 13  16.050 Yes ( 0.30769 0.69231 ) *
                343) Age > 49.5 11   6.702 No ( 0.90909 0.09091 ) *
           43) Price > 122.5 77  55.540 No ( 0.88312 0.11688 )  
             86) CompPrice < 147.5 58  17.400 No ( 0.96552 0.03448 ) *
             87) CompPrice > 147.5 19  25.010 No ( 0.63158 0.36842 )  
              174) Price < 147 12  16.300 Yes ( 0.41667 0.58333 )  
                348) CompPrice < 152.5 7   5.742 Yes ( 0.14286 0.85714 ) *
                349) CompPrice > 152.5 5   5.004 No ( 0.80000 0.20000 ) *
              175) Price > 147 7   0.000 No ( 1.00000 0.00000 ) *
       11) Advertising > 13.5 45  61.830 Yes ( 0.44444 0.55556 )  
         22) Age < 54.5 25  25.020 Yes ( 0.20000 0.80000 )  
           44) CompPrice < 130.5 14  18.250 Yes ( 0.35714 0.64286 )  
             88) Income < 100 9  12.370 No ( 0.55556 0.44444 ) *
             89) Income > 100 5   0.000 Yes ( 0.00000 1.00000 ) *
           45) CompPrice > 130.5 11   0.000 Yes ( 0.00000 1.00000 ) *
         23) Age > 54.5 20  22.490 No ( 0.75000 0.25000 )  
           46) CompPrice < 122.5 10   0.000 No ( 1.00000 0.00000 ) *
           47) CompPrice > 122.5 10  13.860 No ( 0.50000 0.50000 )  
             94) Price < 125 5   0.000 Yes ( 0.00000 1.00000 ) *
             95) Price > 125 5   0.000 No ( 1.00000 0.00000 ) *
    3) ShelveLoc: Good 85  90.330 Yes ( 0.22353 0.77647 )  
      6) Price < 135 68  49.260 Yes ( 0.11765 0.88235 )  
       12) US: No 17  22.070 Yes ( 0.35294 0.64706 )  
         24) Price < 109 8   0.000 Yes ( 0.00000 1.00000 ) *
         25) Price > 109 9  11.460 No ( 0.66667 0.33333 ) *
       13) US: Yes 51  16.880 Yes ( 0.03922 0.96078 ) *
      7) Price > 135 17  22.070 No ( 0.64706 0.35294 )  
       14) Income < 46 6   0.000 No ( 1.00000 0.00000 ) *
       15) Income > 46 11  15.160 Yes ( 0.45455 0.54545 ) *
> #creating train and test data
> set.seed(2)
> train<-sample(1:nrow(Carseats),200)
> 
> Carseats.test<-Carseats[-train,]
> High.test<-High[-train]
> #Building tree on Train data
> tree.carseats1<-tree(High~.-Sales,Carseats,subset = train)
> #apply on test data set
> tree.pred<-predict(tree.carseats1,Carseats.test,type='class')
> table(tree.pred
+       ,High.test)
         High.test
tree.pred No Yes
      No  86  27
      Yes 30  57
> (86+57)/200
[1] 0.715
> #0.715 accuracy predicted
> #see the classification accuracy, dropped from 91% to 71.5% in trained module
> #Summary of Trained model
> summary(tree.carseats1)

Classification tree:
tree(formula = High ~ . - Sales, data = Carseats, subset = train)
Variables actually used in tree construction:
[1] "ShelveLoc"   "Price"       "Income"      "Age"         "Advertising"
[6] "CompPrice"   "Population" 
Number of terminal nodes:  19 
Residual mean deviance:  0.4282 = 77.51 / 181 
Misclassification error rate: 0.105 = 21 / 200 
> #89.5% is of training set, must be tested on unseen
> #data (testing data set)
> 
> #===Pruning==
> set.seed(3)
> cv.carseats<-cv.tree(tree.carseats1, FUN=prune.misclass)
> names(cv.carseats)
[1] "size"   "dev"    "k"      "method"
> cv.carseats
$size
[1] 19 17 14 13  9  7  3  2  1

$dev
[1] 55 55 53 52 50 56 69 65 80

$k
[1]       -Inf  0.0000000  0.6666667  1.0000000  1.7500000  2.0000000  4.2500000
[8]  5.0000000 23.0000000

$method
[1] "misclass"

attr(,"class")
[1] "prune"         "tree.sequence"
> #cv stand for Cross Validation
> #it will create tree with 1-9 terminal nodes 
> # FUN=prune missclass mean classification error should not go down.
> #plotting error
> par(mfrow=c(1,2))
> plot(cv.carseats$size,cv.carseats$dev,
+     type = 'b',col= 'red',
+      lwd = 2)
> plot(cv.carseats$k,cv.carseats$dev,
+      type = 'b',col= 'blue',
+      lwd = 2)
> #Size (number of terminal nodes)and cost complexity factor
> #cost implication is more at the node 9 in first diagram and 1.75 at second diagram
> #Again build tree with 9 terminal  nodes
> #prune the tree to 9 classes
> dev.off()
null device 
          1 
> #the above command will nullify par(mfrow=c(1,2)
> prune.carseats<- prune.misclass(tree.carseats1,best=9)
> plot(prune.carseats)
> text(prune.carseats, pretty = 0)
> tree.pred1<-predict(prune.carseats,Carseats.test,type='class')
> table(tree.pred1,High.test)
          High.test
tree.pred1 No Yes
       No  94  24
       Yes 22  60
> (94+60)/2 #77
[1] 77
> 
> #Bagging is random forest if all predictors
> #are used for building tree
> install.packages("randomForest")
Installing package into ‘C:/Users/Savitha/Documents/R/win-library/3.4’
(as ‘lib’ is unspecified)
trying URL 'https://cran.rstudio.com/bin/windows/contrib/3.4/randomForest_4.6-14.zip'
Content type 'application/zip' length 180846 bytes (176 KB)
downloaded 176 KB

package ‘randomForest’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\Savitha\AppData\Local\Temp\RtmpITQwsB\downloaded_packages
> library(randomForest)
randomForest 4.6-14
Type rfNews() to see new features/changes/bug fixes.
> set.seed(1)
> bag.carseats <- randomForest(High~.-Sales,
+                             Carseats, subset=train,
+                             mtry=10, importance=TRUE)
> dim(Carseats)
[1] 400  12
> importance(bag.carseats)
                    No        Yes MeanDecreaseAccuracy MeanDecreaseGini
CompPrice    6.8632913 -0.7977583             4.595816        8.5850330
Income       0.3328227 -3.9650852            -2.354101        6.7973051
Advertising 15.0634912 13.8553377            19.578109       11.5868694
Population  -1.3222554 -0.2792662            -1.024061        7.8245935
Price       25.6941951 15.5686064            26.890003       25.6301807
ShelveLoc   24.7414425 18.6063885            27.969534       17.4413732
Age          8.2519283  1.6263769             7.156855       12.4048446
Education   -0.4370914 -4.8871921            -3.490403        3.7448229
Urban        2.5550029  0.9287223             2.357068        0.7940307
US           1.6092251  1.0546779             1.964676        0.7898068
> #since our module is using gini index, only refere gini index
> #and take top predictor
> #here it is Price, ShelveLoc, Age,Advertising
> varImpPlot(bag.carseats,col= 'red', pch=10,cex=1.25)
> bag.carseats

Call:
 randomForest(formula = High ~ . - Sales, data = Carseats, mtry = 10,      importance = TRUE, subset = train) 
               Type of random forest: classification
                     Number of trees: 500
No. of variables tried at each split: 10

        OOB estimate of  error rate: 22%
Confusion matrix:
     No Yes class.error
No  106  14   0.1166667
Yes  30  50   0.3750000
> #observe that the OOB error is only 22% (Out of bag=OOB), its (Yes+No)/sum of all
> #which means 79.8% correct classification
> #Test Results
> test.pred.bag <- predict(bag.carseats,
+                          newdata = Carseats[-train,],
+                          type='class')
> table(test.pred.bag,High.test)
             High.test
test.pred.bag No Yes
          No  96  18
          Yes 20  66
> (96+66)/2
[1] 81
> #82% correct classification
> 
> #==================Random Forest===========
> set.seed(1)
> rf.carseats <- randomForest(High~.-Sales,
+                             Carseats, subset = train,
+                             mtry=3, importance = TRUE)
> #same command as bagging, here instead for 10 predictors, 
> #it will square root of 10, which is roughly 3
> dim(Carseats)
[1] 400  12
> importance(rf.carseats)
                    No         Yes MeanDecreaseAccuracy MeanDecreaseGini
CompPrice    3.8076041 -0.46077210            2.5772124         9.555546
Income      -1.6249581 -2.51929639           -2.6630243         8.286403
Advertising 11.3435696 11.92465657           15.0561204        11.450811
Population   1.1742270 -0.83989254            0.2875488         9.420534
Price       21.5101142 18.46444349           25.9775005        21.900185
ShelveLoc   21.4373401 17.23193530           24.9131933        14.605774
Age          5.3043554  2.64010555            5.5088787        11.938031
Education   -2.8318129 -3.15653300           -3.9591462         5.175087
Urban        0.5992869 -0.08054757            0.3102981         1.546324
US          -0.3247941  2.88161124            1.8241833         1.444491
> varImpPlot(rf.carseats,col= 'blue', pch=10,cex=1.25)
> rf.carseats

Call:
 randomForest(formula = High ~ . - Sales, data = Carseats, mtry = 3,      importance = TRUE, subset = train) 
               Type of random forest: classification
                     Number of trees: 500
No. of variables tried at each split: 3

        OOB estimate of  error rate: 21.5%
Confusion matrix:
     No Yes class.error
No  107  13   0.1083333
Yes  30  50   0.3750000
> test.pred.rf <- predict(rf.carseats,
+                          newdata = Carseats[-train,],
+                          type='class')
> table(test.pred.rf,High.test)
            High.test
test.pred.rf  No Yes
         No  100  19
         Yes  16  65
> (100+65)/2
[1] 82.5
> #82.5
