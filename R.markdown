
### get and change directories

    h <- Sys.getenv("HOME")
    d <- "work_dir"
    w <- paste(h, d, sep="/")
    setwd(w)
    getwd()

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

### convert data in a `data.frame` to be categorical

    detach(juul)
    juul$sex <- factor(juul$sex, labels=c("M", "F"))
    juul$menarche <- factor(juul$menarche, labels=c("No", "Yes"))
    juul$tanner <- factor(juul$tanner, labels=c("I", "II", "III", "IV", "V"))
    attach(juul)

