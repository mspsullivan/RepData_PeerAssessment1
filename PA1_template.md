# Reproducible Research: Peer Assessment 1
echo = true

## Loading and preprocessing the data

```r
activity <- read.csv("activity.csv")
activity$date <- as.Date(activity$date)
processedActivity <- aggregate(steps ~ date, data = activity, sum)
hist(processedActivity$steps)
```

![](PA1_template_files/figure-html/unnamed-chunk-1-1.png) 
## Instructions
## 1. Calculate the total number of steps taken per day.
## 2. Make a histogram of the total number of steps taken each day.
## 3. Calculate and report the mean and median of the total number of steps taken per day.

## What is mean total number of steps taken per day?


```r
mean(processedActivity$steps)
```

```
## [1] 10766.19
```
## result: 10766.19
## What is the average daily activity pattern?

```r
mean(processedActivity$steps)
```

```
## [1] 10766.19
```
## result 10765

## Are there differences in activity patterns between weekdays and weekends?
## show a histogram of weekends

```r
weekendFactors <- grep ("S", weekdays(processedActivity$date))
weekdayFactors <- grep ("[MTWF]", weekdays(processedActivity$date))
hist(processedActivity[weekendFactors, "steps"])
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png) 

```r
hist(processedActivity[weekdayFactors, "steps"])
```

![](PA1_template_files/figure-html/unnamed-chunk-4-2.png) 
## show a histogram of weekdays
