# Hungarian algorithm (also known as Munkres algorithm).

- Solve the unique lowest-cost assignment problem

- The problem is also known as maximum weight matching in bipartite graphs

## 구현물 

### sklearn.utils.linear_assignment

```python

def linear_assignment(X):
    """Solve the linear assignment problem using the Hungarian algorithm.
    The problem is also known as maximum weight matching in bipartite graphs.
    The method is also known as the Munkres or Kuhn-Munkres algorithm.
    Parameters
    ----------
    X : array
        The cost matrix of the bipartite graph
    Returns
    -------
    indices : array
        The pairs of (row, col) indices in the original array giving
        the original ordering.
    References
    
# https://github.com/scikit-learn/scikit-learn/blob/master/sklearn/utils/linear_assignment_.py
```


### [scipy.optimize.linear_sum_assignment](https://docs.scipy.org/doc/scipy-0.18.1/reference/generated/scipy.optimize.linear_sum_assignment.html)