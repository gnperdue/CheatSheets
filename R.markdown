## Sources

* Introduction to Probability, by J. Blitzstein and J. Hwang
* Introduction to Statistical Learning with Applications in R, by G. James,
D. Witten, T. Hastie, and R. Tibshirani
* Learning R, by R. Cotton

### clean up

    rm(list=ls())

### environment

    load("PATH/.RData")

### move to a working area

    home <- Sys.getenv("HOME")
    work <- "Dropbox/Programming/Programming/R/LearningR/lrCha09"
    directory <- paste(home, work, sep="/")
    setwd(directory)

### look at datasets

    data()
    data(package = .packages(all.available = TRUE))

### get and change directories

    h <- Sys.getenv("HOME")
    d <- "work_dir"
    w <- paste(h, d, sep="/")
    setwd(w)
    getwd()

### list package contents and/or directory contents

    list.files("/Users/perdue/Library/R/3.0/library/learningr")
    list.files(system.file(package="learningr"))
    list.files(system.file("extdata", package="learningr"))

### read and write csv files

    ?write.csv
    write.csv(thuesen, file="Data/thuesen_gnp.csv")
    ?read.csv
    df = read.csv("Data/thuesen_gnp.csv", header=T)

### basic summary statistics

    x <- rnorm(50)
    mean(x)      # must supply `na.rm=T` to ignore NA
    sd(x)
    var(x)
    median(x)
    quantile(x)
    summary(x)
    str(x)

### missing entries

    any(is.na(x))
    y <- na.omit(x)
    mydf <- na.omit(mydf)
    complete.cases(x)
    !complete.cases(x)
    x[!complete.cases(x)]
    x[complete.cases(x)]

### simple histograms

    x <- rnorm(50)
    hist(x)
    mid.age <- c(2.5, 7.5, 13, 16.5, 17.5, 19, 22.5, 44.5, 70.5)
    acc.count <- c(28, 46, 58, 20, 31, 64, 149, 316, 103)
    age.acc <- rep(mid.age, acc.count)
    brk <- c(0, 5, 10, 16, 17, 18, 20, 25, 60, 80)
    hist(age.acc, breaks=brk)   # defaults to `freq=F`

### empirical cummulative distribution

    x <- rnorm(50)
    n <- length(x)
    plot(sort(x), (1:n)/n, type="s", ylim=c(0, 1))

### q-q plots

    x <- rnorm(50)
    qqnorm(x)

### remove a column from a data.frame

    mydf$column_name <- NULL

### remove rows from a data.frame

    v <- -(10:85)      # vector of elements to remove
    auto <- auto[v,]   # note the comma!

### scatter plots

    pairs(auto[,1:10])

### convert data in a `data.frame` to be categorical

    detach(juul)
    juul$sex <- factor(juul$sex, labels=c("M", "F"))
    juul$menarche <- factor(juul$menarche, labels=c("No", "Yes"))
    juul$tanner <- factor(juul$tanner, labels=c("I", "II", "III", "IV", "V"))
    attach(juul)

### sample a vector

    n <- 10; k <- 5
    sample(n,k)  # sample(n,n) == sample(n)
    x <- 11:20
    x[sample(length(x))]   # 11-20 in random order
    x[sample(length(x), replace=T)]

### get a random set of numbers

    sample(letters, 7)

### get a sample with non-uniform probabilities

    sample(4, 3, replace=T, prob=c(0.1, 0.2, 0.3, 0.4))

### demontmort simulation in three lines of R

    n <- 100
    r <- replicate(10^4, sum(sample(n)==1:n)
    sum(r>=1)/10^4

### the "classic" birthday problem in two lines of R

    # we can do it in one line with `pbirthday()` and `qbirthday()`
    r <- replicate(10^4, max(tabulate(sample(1:365, 23, replace=T))))
    sum(r>=2)/10^4

### replication

* `rep()` repeats input several times
* `replicate()` calls an expression several times

### simple regression

Including prediction and confidence intervals:

    attach(Auto)
    autolm <- lm(mpg~horsepower)
    summary(autolm)
    plot(x=horsepower, y=mpg)
    abline(autolm)
    predict(autolm, data.frame(horsepower=c(98)), interval="confidence")
    predict(autolm, data.frame(horsepower=c(98)), interval="prediction")
    plot(predict(autolm), residuals(autolm))
    plot(predict(autolm), rstudent(autolm))

### multiple regression

Non-linear transformations of predictors: use `I()` (`^` has special meaning in
a formula):

    linmod <- lm(y ~ x + I(x^2))

Confidence intervals:

    confint(fit, 'parameter', level=0.95)

Check residuals:

    par(mfrow=c(2,2))
    plot(fit)

### change the number of panels in the plotting window

    par(mfrow=c(2,2))
    par(mfrow=c(1,1))


### save a pdf of a plot

    pdftitle <- sprintf("plot_%d.pdf", num)
    pdf(pdftitle)
    plot(x,y)
    dev.off()

### slicing

* All rows with a variable in a range:

        cdc[cdc$weight<highwt & cdc$weight > lowwt,]

* Row 1, Column 1, Row 1-Column 1

        cdc[1,]
        cdc[,1]
        cdc[1,1]

### ranges with arbitrary steps

    x <- seq(-10, 10, 2)

### dates and times

    > strftime(now_ct)
    [1] "2015-04-21 08:41:52"
    > strftime(now_ct, "It's %B %Y")
    [1] "It's April 2015"

Create a date with `lubridate`:

    my_date <- ymd("2016-01 01")
    my_date + years(1)   # period
    my_date + dyears(1)  # duration

### adding and replacing columns

    # add a column
    english_monarchs$length.of.reign.years <-
      english_monarchs$end.of.reign - english_monarchs$start.of.reign
    # nicer
    english_monarchs$length.of.reign.years <- with(
      english_monarchs,
      end.of.reign - start.of.reign
    )
    # possibly nicer
    english_monarchs <- within(
      english_monarchs,
      {length.of.reign.years <- end.of.reign - start.of.reign}
    )
    # using plyr...
    # `mutate` accepts new and revised columns as name-value pairs
    english_monarch <- mutate(
      english_monarchs,
      length.of.reign.years=end.of.reign - start.of.reign,
      reign.was.more.than.30.years=length.of.reign.years>30
    )
