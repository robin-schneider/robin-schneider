---
layout: page
title: gymCICY
description: An OpenAI gym for studying heterotic line bundle models.
img: assets/img/pregame.png
importance: 1
category: work
---

Heterotic line bundle models are the [most](https://arxiv.org/abs/1810.00444) succesful construction of realistic compactification for the heterotic string. The number of configurations to consider in systematic scans scales exponentially with $$h^{(1,1)}$$. Hence, for larger values smart ways are needed to parse the landscape of possible configurations.

#### The Package

[gymCICY](https://github.com/robin-schneider/gymCICY) lets you explore heterotic line bundle models via the successfull OpenAI [gym](https://gym.openai.com/) interface. This python package contains two different settings to construct sums of line bundles. First, the `stacking` environment, which simulates the systematic construction of line bundle sums via stacking of five line bundles. Second, in `flipping` agents interact with the charges of the line bundles by either increasing or decreasing them with $$\pm 1$$. You can install the package with

```console
pip install --user git+https://github.com/robin-schneider/gymCICY
```

it uses the [pyCICY](https://github.com/robin-schneider/CICY) package for the reward-computations.

