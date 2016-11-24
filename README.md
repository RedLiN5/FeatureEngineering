FeatureEngineering
My personal feature engineering scripts.

This file contains feature engineering tools, which may be used in the future, in Python files.

## Standardize
``` Python
from sklearn.preprocessing import StandardScaler

StandardScaler().fit_transform(X)
```

## Scaler
```tex
x^' = \frac{x - min(x)}{S}
```

```Python
from sklearn.preprocessing import MinMaxScaler

MinMaxScaler().fit_trainform(X)
```

# Feature Selection
## Variance Selection
``` Python
from sklearn.feature_selection import VarianceThreshold

VarianceThreshold(threshold = 3).fit_transform(X)
```

## Pearson's Correlation
```Python
from sklearn.feature_selection import SelectKBest
from scipy.state import pearsonr
import pandas as pd

def KBest(X, y, k):
        pearsons = np.array(map(lambda x: pearsonr(x, y), X.T))
        nrow = pearsons.shape[0]
        combine = np.hstack((pearsons, np.zeros((nrow, 1))))
        combine[:,-1] = range(nrow)
        columns = ['pearson', 'pvalue', 'position']
        combine = pd.DataFrame(combine, columns = columns)
        combine_sort = combine.sort_values('pvalue').reset_index(drop=True)
        pos = map(int, combine_sort.ix[:(k-1), 'position'])
        print X[:, pos]
```

## Maximal Information Coefficient-based Nonparametric Exploration
In some cases, the Pearson's coefficient is not significant, but the pattern still exists. So we use MIC.
```Python
from sklearn.feature_selection import SelectKBest
from minepy import MINE

def mic(x, y):
	m = MINE()
	m.compute_score(x, y)
	return (m.mic(), .5)

kbest = SelectKBest(lambda X, Y: np.array(map(lambda x: mic(x, Y), X.T)).T, k=2)
kbest.fit_transform(X, y)
kbest.scores_
```

