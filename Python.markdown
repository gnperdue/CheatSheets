
### Simple Plot with Two Curves on the Same Subplot

    X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
    C, S = np.cos(X), np.sin(X)
    plt.plot(X,C)
    plt.plot(X,S)
    plt.show()

### Custom Plot with Two Curves on the Same Subplot

    # create a new figure of size 8x6 inches, 80 dots per inch
    plt.figure(figsize=(8, 6), dpi=80)
    # create a new subplot from a grid of 1x1
    plt.subplot(1, 1, 1)
    plt.plot(X, C, color="blue", linewidth=1.0, linestyle="-")
    plt.plot(X, S, color="green", linewidth=1.0, linestyle="-")
    plt.xlim(X.min() * 1.1, X.max() * 1.1)
    plt.ylim(C.min() * 1.1, C.max() * 1.1)
    plt.xticks(np.linspace(-4, 4, 9, endpoint=True))
    plt.yticks(np.linspace(-1, 1, 5, endpoint=True))
    # or ...
    # plt.xticks([-np.pi, -np.pi/2, 0, np.pi/2, np.pi],
    #            [r'$-\pi$', r'$-\pi/2$', r'$0$', r'$+\pi/2$', r'$+\pi'$])
    # plt.yticks([-1, 0, +1], [r'$-1$', r'$0$', r'$+1$'])
    # `gca` stands for "get current axis"
    ax = plt.gca()
    ax.spines['right'].set_color('none')
    ax.spines['top'].set_color('none')
    ax.xaxis.set_ticks_position('bottom')
    ax.spines['bottom'].set_position(('data', 0))
    ax.spines['left'].set_position(('data', 0))
    ax.yaxis.set_ticks_position('left')
    savefig("exercise_2.png", dpi=72)
    show()

### Plot with a Legend

    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plot1, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="-")
    plt.legend([plot1], loc='upper left')
    plt.show()

### Annotate Points

    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plot1, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="-")
    t = 2 * np.pi / 3
    # here, the `cos(t)` is the function we're using, etc.
    plot1, = plt.plot([t, t], [0, np.cos(t)], color='blue', linewidth=2.5, 
                      linestyle='--')
    plt.scatter([t, ], [np.cos(t), ], 50, color='blue')
    plt.annotate(r'$sin(\frac{2\pi}{3})=\frac{\sqrt{3}}{2}$',
                 xy=(t, np.sin(t)), xycoords='data',
                 xytext=(+10, +30), textcoords='offset points', 
                 fontsize=16, arrowprops=dict(arrowstyle="->", 
                                              connectionstyle="arc3,rad=.2"))
    # here, the `sin(t)` is the function we're using, etc.
    plot1, = plt.plot([t, t], [0, np.sin(t)], color='red', linewidth=2.5,
                      linestyle='--')
    plt.scatter([t, ], [np.sin(t), ], 50, color='red')
    plt.annotate(r'$cos(\frac{2\pi}{3})=-\frac{1}{2}$',
                 xy=(t, np.cos(t)), xycoords='data',
                 xytext=(-90, -50), textcoords='offset points', 
                 fontsize=16, arrowprops=dict(arrowstyle="->", 
                                              connectionstyle="arc3,rad=.2"))
    plt.show()

### Enlarge Tick Labels

    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plot1, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="-")
    ax = plt.gca()
    for label in ax.get_xticklabels() + ax.get_yticklabels():
        label.set_fontsize(16)
        label.set_bbox(dict(facecolor='white', edgecolor='None', alpha=0.65))
    plt.show()

### Multiple Plots in a Grid

    fig = plt.figure(1)
    fig.subplots_adjust(bottom=0.025, left=0.025, top=0.975, right=0.975)
    plt.subplot(2, 1, 1)
    plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plt.subplot(2, 3, 4)
    plt.plot(X, C, color="red", linewidth=2.5, linestyle="--")
    plt.subplot(2, 3, 5)
    plt.plot(X, S, color="blue", linewidth=2.5, linestyle="-")
    plt.subplot(2, 3, 6)
    plt.plot(X, S, color="red", linewidth=2.5, linestyle="--")
    # plt.show()    # required sometimes, not others... ?
    # plt.close(1)  # makes it go away

### Multiplots with Custom Axes (Start)

    X = np.linspace(-2.0 * np.pi, 2.0 * np.pi, 256, endpoint=True)
    C, S = np.cos(X), np.sin(X)
    
    fig = plt.figure(1)
    fig.subplots_adjust(bottom=0.025, left=0.025, top=0.975, right=0.975)
    
    ax1 = plt.subplot(2, 1, 1)
    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plt.legend([plot1], loc='upper left')
    ax1.set_xlim([X.min() * 0.75, X.max() * 1.1])
    ax1.set_ylim([C.min() * 1.1, C.max() * 1.4])
    
    #plt.subplot(2, 3, 4)
    #plt.plot(X, C, color="red", linewidth=2.5, linestyle="--")
    
    #plt.subplot(2, 3, 5)
    #plt.plot(X, S, color="blue", linewidth=2.5, linestyle="-")
    
    #plt.subplot(2, 3, 6)
    #plt.plot(X, S, color="red", linewidth=2.5, linestyle="--")
    
    # plt.close(1)  # makes it go away

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
