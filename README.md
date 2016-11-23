FeatureEngineering
My personal feature engineering scripts.

This file contains feature engineering tools, which may be used in the future, in Python files.

## Standardize
``` Python
from sklearn.preprocessing import StandardScaler

StandardScaler().fit_transform(X)
```

## Scaler
$$
\begin{aligned*}
x^' = \frac{x - min(x)}{S}
\end{aligned*}
$$

```Python
from sklearn.preprocessing import MinMaxScaler

MinMaxScaler().fit_trainform(X)
```

