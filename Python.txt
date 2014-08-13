
### Summary Statistics with SciPy

    from scipy.stats import norm
    x = norm.rvs(size=50)
    np.mean(x)     # Python skips NaN by default
    np.var(x)
    np.std(x)
    np.median(x)
    np.percentile(x, [0, 25, 50, 75, 100])

### Read a CSV with Pandas

    import os
    import pandas as pd
    from pandas import DataFrame, Series
    path = os.environ['HOME'] + '/Data/'
    filename = path + 'the_data.csv'
    df = pd.read_csv(filename)
    np.mean(df.ivar)
    df.ivar.mean()
    df.ivar.describe()        # Summary statistics

### Histogram Data

    import matplotlib.pyplot as plt
    from scipy.stats import norm
    x = norm.rvs(size=50)
    plt.hist(x)
    mid_age = np.array([2.5, 7.5, 13, 16.5, 17.5, 19, 22.5, 44.5, 70.5])
    acc_count = np.array([28, 46, 58, 20, 31, 64, 149, 316, 103])
    age_acc = np.repeat(mid_age, acc_count)   # Similar to R's `rep`
    brk = [0, 5, 10, 16, 17, 18, 20, 25, 60, 80]
    plt.hist(age_acc, bins=brk)  # R defaults to density plot; now Python
    plt.hist(age_acc, bins=brk, normed=True)  # area of column prop-to number

### Empirical Cumulative Distribution

    n = len(x)
    plt.plot(np.sort(x), np.arange(1, n + 1) / float(n))

### Q-Q Plots

    import statsmodels.api as sm
    sm.qqplot(x, line='45')

### Boxplots

    spread = np.random.rand(50) * 100
    center = np.ones(25) * 40
    flier_high = np.random.rand(10) * 100 + 100
    flier_low = np.random.rand(10) * -100
    data = np.concatenate((spread, center, flier_high, flier_low), 0)
    boxplot(data)

### Summary Statistics by Groups

    path = '/Library/Frameworks/R.framework/Versions/3.0/'
    path += 'Resources/library/ISwR/rawdata/'
    filename = path + 'stroke.csv'
    jdf.groupby(['tanner']).mean()
    jdf.groupby(['tanner']).mean().igf1
    jgrouped = jdf.groupby(['tanner'])
    jgrouped.agg(mean)
