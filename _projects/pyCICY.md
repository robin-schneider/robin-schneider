---
layout: page
title: pyCICY
description: A python CICY toolkit.
img: /assets/img/calabiyau.jpg
importance: 1
category: work
---

Calabi-Yau manifolds are an important ingredient in string theory compactifications. Their topological quantities can be related to for example the number of massless fermion generations in the four-dimensional theory. Complete Intersection Calabi-Yau (CICY) manifolds are one of the most common constructions. There are 7890 three-folds and almost a million four-folds.

#### The package

[pyCICY](https://github.com/robin-schneider/CICY) lets you compute various quantites, such as Chern classes, triple intersection numbers or Hodge numbers of tangent and line bundles. It's a python package mostly utilizing [numpy](https://numpy.org/) for the underlying computations. Installation is straightforwad with [pip](https://pypi.org/project/pip/). For the latest version install from github

```console
pip install --user git+https://github.com/robin-schneider/CICY
```

#### The Quintic

Take for example the quintic manifold given by a homogeneous polynomial of degree five in $$\mathbb{P}^4$$:

$$
\mathcal{Q} \in [4|5]
$$

We import the `CICY` module

```python
from pyCICY import CICY
import numpy as np
```

define the configuration matrix as a numpy array and initialize a new CICY object

```python
configuration_matrix = np.array([[4,5]])
quintic = CICY(configuration_matrix)
```

Next we can compute the Hodge numbers of a line bundle

$$
h^\bullet (\mathcal{Q}, \mathcal{O}(3)) = (35,0,0,0)
$$

with

```python
line_bundle = [3]
quintic.line_co(line_bundle)
>>> array([35.,  0.,  0.,  0.])
```

For a full list of functionality run:

```python
help(M)
```
