
### module auto reload in ipython

```
%load_ext autoreload
%autoreload 2
```

### installing stuff

If you use a `setup.py install` approach, do it like this:

    $ python setup.py install --record files.txt
    $ cat files.txt | xargs rm -rf  # this will remove all the installed files

### get module location

1. either `python -v`, then `import module_name`, or
2. `print(sys.modules.items())`

### check versions

    import numpy as np
    print('numpy version: {}'.format(np.__version__))

### meta info

    dir(<function name>)      # attributes of a function
    dir(<object name>)        # attributes of a object
    <function name>.__doc__   # see docstrings (sometimes, won't work for `+`, etc.)
                              # for `+`, use `from operator import add`
    help(<function/object name>)
    type(<function/object name>)   # trouble with, e.g., `int` (how to `int()`?)

### quiet warnings

    import warnings
    # 'error' to stop on warns, 'ignore' to ignore silly matplotlib noise
    warnings.filterwarnings('ignore')

### debugger tricks in ipython

    import pdb
    ipdb = pdb.Pdb()
    ipdb.runcall(is_chain, chain, 5)  # fn, arg1, arg2, etc.

In IPython:

    run -d myscript.py
    run -d -b20 myscript.py <args>   # break at line 20
    ll                               # long list

Debug a function w/o `ipdb`:

    from IPython.core.debugger import Pdb; ipdb=Pdb()
    ipdb.runcall(myfn, myarg1, myarg2)

Can also just do this with `pdb`:

    import pdb
    pdb.runcall(myfn, myarg1, myarg2)

Also, in code

    import pdb; pdb.set_trace()
    # Python 3.7 - repace this with `breakpoint()` (new built-in)

Breakpoint in another module

    import sys
    sys.path.append("/full/path/to/module")
    import module
    b module:<line>

### indexing tricks

    idx = np.zeros(50)
    idx[np.flatnonzero(f['exclusive-signal'][:50])] = 1

### simple matplotlib plot with two curves on the same subplot

    X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
    C, S = np.cos(X), np.sin(X)
    plt.plot(X,C)
    plt.plot(X,S)
    plt.show()

### simple matplotlib scatter plot

    plt.scatter(x, y, color='blue', marker='o')
    plt.title('Y vs X')
    plt.xlabel('X (units)')
    plt.ylabel('Y (units)')
    plt.axis([0, 105, 0, 80])
    plt.show()

### simple matplotlib legend example

    xs = [x / 10.0 for x in range(-50, 50)]
    plt.plot(xs, [scipy.stats.norm.pdf(x, scale=1) for x in xs],
             '-', label='mu=0, sigma=1')
    plt.plot(xs, [scipy.stats.norm.pdf(x, scale=2) for x in xs],
             '--', label='mu=0, sigma=2')
    plt.plot(xs, [scipy.stats.norm.pdf(x, scale=0.5) for x in xs],
             ':', label='mu=0, sigma=0.5')
    plt.plot(xs, [scipy.stats.norm.pdf(x, loc=-1) for x in xs],
             '-.', label='mu=-1, sigma=1')
    plt.legend()
    plt.title('Various Normal PDFs')
    plt.show()

### custom plot with two curves on the same subplot

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

### plot with a legend

    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plot1, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="-")
    plt.legend([plot1], loc='upper left')
    plt.show()

### annotate points

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

### enlarge tick labels

    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plot1, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="-")
    ax = plt.gca()
    for label in ax.get_xticklabels() + ax.get_yticklabels():
        label.set_fontsize(16)
        label.set_bbox(dict(facecolor='white', edgecolor='None', alpha=0.65))
    plt.show()

### multiple plots in a grid

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

### equal axes

    plt.plot(xx, yy)    # xx = whatever, etc.
    plt.axes().set_aspect('equal', 'datalim')

### multiplots with custom axes 

    X = np.linspace(-2.0 * np.pi, 2.0 * np.pi, 256, endpoint=True)
    C, S = np.cos(X), np.sin(X)
    
    fig = plt.figure(1)
    fig.subplots_adjust(bottom=0.025, left=0.025, top=0.975, right=0.975)
    
    ax1 = plt.subplot(2, 1, 1)
    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plt.legend([plot1], loc='upper left')
    ax1.set_xlim([X.min() * 0.75, X.max() * 1.1])
    ax1.set_ylim([C.min() * 1.1, C.max() * 1.4])
    
    ax2 = plt.subplot(2, 3, 4)
    plot2, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="--")
    plt.legend([plot2], loc='lower right')
    ax2.set_xlim([X.min() * 1.25, X.max() * 0.75])
    ax2.set_ylim([S.min() * 1.8, S.max() * 1.1])
    
    ax3 = plt.subplot(2, 3, 5)
    plot3, = plt.plot(X, S, color="blue", linewidth=2.5, linestyle="-")
    plt.legend([plot2], loc='lower left')
    ax3.set_xlim([X.min() * 1.1, X.max() * 1.1])
    ax3.set_ylim([S.min() * 1.1, S.max() * 1.1])
    
    ax4 = plt.subplot(2, 3, 6)
    plot4, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="--")
    ax4.set_xlim([X.min() * 1.1, X.max() * 1.1])
    ax4.set_ylim([S.min() * 1.5, S.max() * 1.5])
    
    # plt.close(1)  # makes it go away

### multiple histograms on the same figure

    ax1 = plt.subplot(2, 1, 1)
    plt.hist(np.array(expend_lean))
    ax2 = plt.subplot(2, 1, 2)
    plt.hist(np.array(expend_obese))
    plt.show()

### custom ticks and grid

    X = np.linspace(-2.0 * np.pi, 2.0 * np.pi, 256, endpoint=True)
    C, S = np.cos(X), np.sin(X)
    fig = plt.figure(1, figsize=(12, 16))
    fig.subplots_adjust(bottom=0.025, left=0.025, top=0.975, right=0.975)
    ax1 = plt.subplot(2, 1, 1)
    plot1, = plt.plot(X, C, color="blue", linewidth=2.5, linestyle="-")
    plot1, = plt.plot(X, S, color="red", linewidth=2.5, linestyle="-")
    ax1.set_xlim([X.min() * 1.1, X.max() * 1.1])
    ax1.set_ylim([C.min() * 1.1, C.max() * 1.1])
    ax1.xaxis.set_major_locator(plt.MultipleLocator(1.0))
    ax1.yaxis.set_major_locator(plt.MultipleLocator(1.0))
    ax1.xaxis.set_minor_locator(plt.MultipleLocator(0.1))
    ax1.yaxis.set_minor_locator(plt.MultipleLocator(0.1))
    ax1.grid(which='major', axis='x', linewidth=0.75, linestyle='-', color='0.75')
    ax1.grid(which='major', axis='y', linewidth=0.25, linestyle='-', color='0.75')
    ax1.grid(which='minor', axis='x', linewidth=0.75, linestyle='-', color='0.75')
    ax1.grid(which='minor', axis='y', linewidth=0.25, linestyle='-', color='0.75')
    ax1.set_yticklabels([])

### summary statistics with sciPy

    from scipy.stats import norm
    x = norm.rvs(size=50)
    np.mean(x)     # Python skips NaN by default
    np.var(x)
    np.std(x)
    np.median(x)
    np.percentile(x, [0, 25, 50, 75, 100])
    norm.interval(0.95)      # tuple with 95% CL endpoints
    norm.interval(0.95, loc=mu, scale=scipy.stats.sem(x)) 
    norm.ppf(0.025)          # equiv to R qnorm(0.25)
    np.asarray([norm.ppf(0.025), norm.ppf(0.975)])

### making a Pandas `DataFrame` from `Series`

    nev = pd.Series({'viro failure': 26, 'no failure': 94})
    lop = pd.Series({'viro failure': 10, 'no failure': 110})
    df = pd.DataFrame({'nevaripine': nev, 'lopinavir': lop})

### making a Pandas `DataFrame` from a NumPy array

    df = pd.DataFrame(np.array([[40, 100], [30, 120]]),
                      columns=['quit', 'not-quit'], 
                      index=['support grp', 'no support'])

### chi2 test of independence in a contingency table (here, Pandas `DataFrame`)

Can use any `R x C` table...

    chi2, p, dof, expected = stats.chi2_contingency(df)

### read a csv with Pandas

    import os
    import pandas as pd
    from pandas import DataFrame, Series
    path = os.environ['HOME'] + '/Data/'
    filename = path + 'the_data.csv'
    df = pd.read_csv(filename)
    np.mean(df.ivar)
    df.ivar.mean()
    df.ivar.describe()        # Summary statistics

Use `read_table` instead of `read_csv` to get tsv files, etc.

### read a csv with a datetime index using Pandas

    df = pd.read_csv(filename, parse_dates=True, index_col='Date')
    df.dropna()   # clean out `NaN`s

### plot a count of events binned in time using Pandas

    df = pd.read_csv(filename, parse_dates=True, index_col='Date')
    filtered_df = df[df['Column_name'] == 'value_of_interest']
    filtered_df['Count'] = 1
    filtered_by_day = filtered_df.to_period('D')
    filtered_counted = filtered_by_day.groupby(level=0).count()
    filtered_counted.plot()

### plot categorical activity with a Pandas `DataFrame`

    act = df['Activity']
    unq = act.unique()
    df['Category'] = 0
    for i in unq:
        df['Category'][df['Activity'] == i] = np.where(unq == i)[0][0]
    df.plot(style='ko')

### drop a column from a Pandas `DataFrame`

    energydf = energydf.drop('Unnamed: 0', 1)  # `1` is the axis

### fill missing data in a Pandas `DataFrame`

    mydf['var'] = mydf['var'].fillna(value)

### exploratory analysis with Pandas `DataFrame`s

Useful summary statistics, etc.

    mydf.head()
    mydf.info()
    mydf.describe()
    mydf['my_attribute'].value_counts()
    mydf.hist(bins=N, figsize=(W, H))     # plus, plt.show(), etc.

### histogram data with Matplotlib

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

### plot categorical data in a pandas `DataFrame`

    mydf['var'].value_counts()
    mydf['var'].value_counts().plot(kind='bar')

### empirical cumulative distribution

    n = len(x)
    plt.plot(np.sort(x), np.arange(1, n + 1) / float(n))

### Q-Q plots

    import statsmodels.api as sm
    sm.qqplot(x, line='45')

### boxplots

    spread = np.random.rand(50) * 100
    center = np.ones(25) * 40
    flier_high = np.random.rand(10) * 100 + 100
    flier_low = np.random.rand(10) * -100
    data = np.concatenate((spread, center, flier_high, flier_low), 0)
    boxplot(data)

### summary statistics by groups

    path = '/Library/Frameworks/R.framework/Versions/3.0/'
    path += 'Resources/library/ISwR/rawdata/'
    filename = path + 'stroke.csv'
    jdf.groupby(['tanner']).mean()
    jdf.groupby(['tanner']).mean().igf1
    jgrouped = jdf.groupby(['tanner'])
    jgrouped.agg(mean)

### logistic regression

    import statsmodels.api as sm
    logit = sm.Logit(data['to_predict'], data[train_cols])  # data is a DataFrame
    result = logit.fit()
    print result.summary()
    print result.conf_int()
    print np.exp(result.params)  # odds ratios

### `display` images in IPython notebook

    from IPython.display import display, Image
    test_image = Image('full_path/to/file.png')
    display(test_image)

### build a mesh

    xx = np.linspace(0, 5, 6)
    yy = np.linspace(0, 5, 6)
    xy1, xy2 = np.meshgrid(xx, yy)
    [t for t in zip(xy1.flat, xy2.flat)]

### row-column conventions

    xs = []
    ys = []
    for row_i in range(img.shape[0]):
        for col_i in range(img.shape[1]):
            xs.append([row_i, col_i])
            ys.append(img[row_i, col_i])

### check the type of an object without importing the associated module

```
import sys
def is_dataframe(x):
    return isinstance(x, getattr(sys.modules.get('pandas'), 'DataFrame', None))
```

### proper figure resizing in a Jupyter notebook

```
from IPython.core.pylabtools import figsize
figsize(11, 9)
```
