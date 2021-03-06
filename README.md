# TensorFlow ManOpt

[![PyPI version](https://img.shields.io/pypi/v/tensorflow-manopt.svg)](https://pypi.org/project/tensorflow-manopt/)
[![DOI](https://zenodo.org/badge/298014876.svg)](https://zenodo.org/badge/latestdoi/298014876)
[![Build Status](https://travis-ci.org/master/tensorflow-manopt.svg?branch=master)](https://travis-ci.org/master/tensorflow-manopt)
[![Coverage Status](https://coveralls.io/repos/github/master/tensorflow-manopt/badge.svg?branch=master)](https://coveralls.io/github/master/tensorflow-manopt?branch=master)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/python/black)
[![License](https://img.shields.io/:license-mit-blue.svg)](https://badges.mit-license.org)

A library for manifold-constrained optimization in TensorFlow.

## Installation

To install the latest development version from GitHub:

```bash
pip install git+https://github.com/master/tensorflow-manopt.git
```

To install a package from PyPI:

```bash
pip install tensorflow-manopt
```

## Features

The core package implements concepts in differential geometry, such as
manifolds and Riemannian metrics with associated exponential and logarithmic
maps, geodesics, retractions, and transports. For manifolds, where closed-form
expressions are not available, the library provides numerical approximations.

<img align="right" width="400" src="https://github.com/master/tensorflow-manopt/blob/master/examples/usage.png?raw=true">

```python
S = manopt.manifolds.Sphere()

x = S.projx(tf.constant([0.1, -0.1, 0.1]))
u = S.proju(x, tf.constant([1., 1., 1.]))
v = S.proju(x, tf.constant([-0.7, -1.4, 1.4]))

y = S.exp(x, v)

u_ = S.transp(x, y, u)
v_ = S.transp(x, y, v)
```

### Manifolds

 - `manifolds.Cholesky` - manifold of lower triangular matrices with positive diagonal elements
 - `manifolds.Euclidian` - unconstrained manifold with the Euclidean metric
 - `manifolds.Grassmannian` - manifold of `p`-dimensional linear subspaces of the `n`-dimensional space
 - `manifolds.Hyperboloid` - manifold of `n`-dimensional hyperbolic space embedded in the `n+1`-dimensional Minkowski space
 - `manifolds.Poincare` - the Poincaré ball model of the hyperbolic space
 - `manifolds.Product` - Cartesian product of manifolds
 - `manifolds.SPDAffineInvariant` - manifold of symmetric positive definite (SPD) matrices endowed with the affine-invariant metric
 - `manifolds.SPDLogCholesky` - SPD manifold with the Log-Cholesky metric
 - `manifolds.SPDLogEuclidean` - SPD manifold with the Log-Euclidean metric
 - `manifolds.SpecialOrthogonal` - manifold of rotation matrices
 - `manifolds.Sphere` - manifold of unit-normalized points
 - `manifolds.StiefelEuclidean` - manifold of orthonormal `p`-frames in the `n`-dimensional space endowed with the Euclidean metric
 - `manifolds.StiefelCanonical` - Stiefel manifold with the canonical metric
 - `manifolds.StiefelCayley` - Stiefel manifold the retraction map via an iterative Cayley transform


### Optimizers

 Constrained optimization algorithms work as drop-in replacements for Keras
optimizers for sparse and dense updates in both Eager and Graph modes.

 - `optimizers.RiemannianSGD` - Riemannian Gradient Descent
 - `optimizers.RiemannianAdam` - Riemannian Adam and AMSGrad
 - `optimizers.ConstrainedRMSProp` - Constrained RMSProp

### Layers

 - `layers.ManifoldEmbedding` - constrained `keras.layers.Embedding` layer

## Examples

 - [SPDNet](examples/spdnet/) - Huang, Zhiwu, and Luc Van Gool. "A Riemannian network for SPD matrix learning." Proceedings of the Thirty-First AAAI Conference on Artificial Intelligence. AAAI Press, 2017.
 - [LieNet](examples/lienet/) - Huang, Zhiwu, et al. "Deep learning on Lie groups for skeleton-based action recognition." Proceedings of the IEEE conference on computer vision and pattern recognition. 2017.
 - [GrNet](examples/grnet/) - Huang, Zhiwu, Jiqing Wu, and Luc Van Gool. "Building Deep Networks on Grassmann Manifolds." AAAI. AAAI Press, 2018.
 - [Hyperbolic Neural Network](examples/hyperbolic_nn/) - Ganea, Octavian, Gary Bécigneul, and Thomas Hofmann. "Hyperbolic neural networks." Advances in neural information processing systems. 2018.
 - [Poincaré GloVe](examples/poincare_glove/) - Tifrea, Alexandru, Gary Becigneul, and Octavian-Eugen Ganea. "Poincaré Glove: Hyperbolic Word Embeddings." International Conference on Learning Representations. 2018.

## References

 If you find TensorFlow ManOpt useful in your research, please cite:

```
@software{tfmanopt2020smirnov,
  author       = {Oleg Smirnov},
  title        = {{TensorFlow ManOpt: a library for manifold-
                   constrained optimization in TensorFlow}},
  month        = oct,
  year         = 2020,
  publisher    = {Zenodo},
  version      = {v0.1.0},
  doi          = {10.5281/zenodo.4094937},
  url          = {https://doi.org/10.5281/zenodo.4094937}
}

```

## Acknowledgment

 TensorFlow ManOpt was inspired by many similar projects:

 - [Manopt](https://www.manopt.org/), a matlab toolbox for optimization on manifolds
 - [Pymanopt](https://www.pymanopt.org/), a Python toolbox for optimization on manifolds
 - [Geoopt](https://geoopt.readthedocs.io/): Riemannian Optimization in PyTorch
 - [Geomstats](https://geomstats.github.io/), an open-source Python package for computations and statistics on nonlinear manifolds

## License

 The code is MIT-licensed.
