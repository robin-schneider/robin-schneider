---
layout: page
title: cymetric
description: A python library for studying Calabi-Yau metrics.
img: assets/img/calabiyau_metric.jpg
importance: 1
category: work
---

[cymetric](https://github.com/pythoncymetric/cymetric) is a Python package for learning of moduli-dependent Calabi-Yau metrics using neural networks implemented in TensorFlow. Install with

```console
pip install git+https://github.com/pythoncymetric/cymetric
```

It consists of two modules

1. One for generating points containing **PointGenerator**s for CICYs and hypersurfaces in toric varieties from the Kreuzer-Skarke list.
2. A collection of various tensorflow models learning corrections to the Fubini-Study metric.

### The PointGenerator

Here is an example for the Fermat Quintic.

```python
import numpy as np
from cymetric.pointgen.pointgen import PointGenerator
monomials = 5*np.eye(5, dtype=np.int64)
shape_moduli = np.ones(5)
vol_moduli = np.ones(1)
ambient = np.array([4])
dirname = 'fermat'
pg = PointGenerator(monomials, shape_moduli, vol_moduli, ambient)
kappa = pg.prepare_dataset(200000, dirname)
pg.prepare_basis(dirname, kappa = kappa)
```

### The PhiFSModel

is Kähler by construction

$$
g_{CY} = g_{FS} + \partial \bar\partial \phi
$$

and in the same Kähler class as the reference metric when the Kähler loss is enforced. Let's find a metric for the Fermat.

```python
import tensorflow.keras as tfk
from cymetric.models.tfhelper import prepare_tf_basis
from cymetric.models.tfmodels import PhiFSModel
from cymetric.models.metrics import *
data = np.load(dirname+'/dataset.npz'))
BASIS = prepare_tf_basis(np.load(dirname+'/basis.pickle'), allow_pickle=True))
weights = data['y_train'][:,0]
nn = tfk.Sequential([tfk.Input(shape=(10)),
                    tfk.layers.Dense(64, activation='gelu'),
                    tfk.layers.Dense(64, activation='gelu'),
                    tfk.layers.Dense(64, activation='gelu'),
                    tfk.layers.Dense(1, use_bias='False')])
model = PhiFSModel(nn, BASIS, kappa=kappa)
cmetrics = [TotalLoss(), SigmaLoss(), Volkloss()]
model.compile(custom_metrics = cmetrics, optimizer=tfk.optimizers.Adam())
history = model.fit(
    data['X_train'], data['y_train'], epochs=100, batch_size=64,
    validation_split=0.1, verbose=1, sample_weight=weights
    )
```


