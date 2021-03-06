# Reproducible Research: Peer Assessment 1
echo = true

## Loading and preprocessing the data

```r
activity <- read.csv("activity.csv")
```
## Instructions
## 1. Calculate the total number of steps taken per day.
## 2. Make a histogram of the total number of steps taken each day.
## 3. Calculate and report the mean and median of the total number of steps taken per day.
## Here is a histogram for the total number of steps each day.

```r
activity$date <- as.Date(activity$date)
processedActivity <- aggregate(steps ~ date, data = activity, sum)
hist(processedActivity$steps)
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 
## What is mean total number of steps taken per day?


```r
mean(processedActivity$steps)
```

```
## [1] 10766.19
```
## result: 10766.19
## What is the median daily activity pattern?

```r
median(processedActivity$steps)
```

```
## [1] 10765
```
## result 10765

## Here is the 5-minute interval with the maximum number of steps:
## This is really important to note. Was the test subject freaking out? 
## Then we might want to smooth out this data. 
## If the max is just above normal we can make good use of the averages.

```r
max(activity$steps, na.rm = TRUE)
```

```
## [1] 806
```
## Gadzooks. That is really high. Many times the mean of about 37.
## For this data, we need to be cautious using averages.
## Now look at the time series
## Present a time-series plot of steps taken avereged over all of the days

```r
plot(activity$interval, activity$steps, type = "l")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png) 

```r
png(file ="figure/plot1.png")
plot(activity$interval, activity$steps, type = "l")
dev.off()
```

```
## pdf 
##   2
```
## That points out how each day the steps built up during the day
## and dropped off at night.
## Now let's impute missing values.
## Here is the number of missing values:

```r
sum(is.na(processedActivity$steps))
```

```
## [1] 0
```
## Anything over 2300 is over 13%. That's pretty significant.
## Let's 200 steps for each of the values. That should be better than NA.


```r
processedActivity$steps[is.na(processedActivity$steps)] <- 200
```
## Here is a histogram of the total steps taken after replacing NAs

```r
hist(processedActivity$steps)
```

![](PA1_template_files/figure-html/unnamed-chunk-9-1.png) 

```r
png(file ="figure/plot2.png")
hist(processedActivity$steps)
dev.off()
```

```
## pdf 
##   2
```
## Are there differences in activity patterns between weekdays and weekends?
## Here is a histogram of weekend steps:

```r
weekendFactors <- grep ("S", weekdays(processedActivity$date))
weekdayFactors <- grep ("[MTWF]", weekdays(processedActivity$date))
hist(processedActivity[weekendFactors, "steps"])
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png) 
## Now showing a histogram of weekdays:

```r
hist(processedActivity[weekdayFactors, "steps"])
```

![](PA1_template_files/figure-html/unnamed-chunk-11-1.png) 
## Write figures to files

```r
png(file ="figure/plot3.png")
hist(processedActivity[weekendFactors, "steps"])
dev.off()
```

```
## pdf 
##   2
```

```r
png(file ="figure/plot4.png")
hist(processedActivity[weekdayFactors, "steps"])
dev.off()
```

```
## pdf 
##   2
```
