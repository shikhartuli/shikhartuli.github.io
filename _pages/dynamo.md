---
layout: page
permalink: /dynamo/
title: ""
description: ""
nav: false
---

<div align="center">
  <img src="{{ site.baseurl }}/assets/img/dynamo_logo.png" alt="DynaMo" width="80" align="center" />
</div>

<br>

<div align="center">
  <h1>&nbsp;DynaMo: Why Predict Just One Token at a Time?</h1>
</div>

***

<div align="center">
  <a href=""><img src="https://img.shields.io/badge/python-v3.10-blue" alt="Python"></a>
  <a href=""><img src="https://img.shields.io/badge/pytorch-v2.0.1-e74a2b" alt="PyTorch"></a>
  <a href=""><img src="https://img.shields.io/badge/transformers-v4.30.0-8a2be2" alt="Huggingface"></a>
  <a href=""><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fshikhartuli.github.io%2Fdynamo&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false" alt="Hits"></a>
</div>

<br>

DynaMo is a suite of multi-token prediction models. Our models are instantiated using the [Pythia](https://github.com/EleutherAI/pythia) weights. Our models parallely generate multiple tokens using independent token heads.

<div align="center">
  <img src="{{ site.baseurl }}/assets/img/multi_token_intro.png" alt="DynaMo Multi-token Model" width="80%" />
  <br>
  <div align="center" width="80%">
    <em>Multi-token prediction in DynaMo. (a) Traditional autoregressive prediction (one token at a time) requires three forward passes. (b) Non-autoregressive multi-token prediction requires only one forward pass.</em>
  </div>
  <br>
</div>

## Training

We implement training using the modified CLM objective that trains each token head _independently_ using the following loss function:

$$\mathcal{L}_{\text{T}n} = - \frac{1}{N} \sum_{j=1}^N \sum_{t=1}^{T - n + 1} \log p(\mathbf{x}_{t+n}^j|\mathbf{x}_{1:t}^j)$$

for the n<sup>th</sup> token head.

## Multi-token Generation

We propose three novel techniques to execute multi-token generation using the DynaMo models:

- **Dynamic back-off**: We back-off to lower-order n-gram prediction when all the probabilities in the predicted joint probability distribution fall below a threshold.
- **Adaptive thresholding**: We implement adaptive thresholding of the estimated joint probability distribution to further boost performance.
- **Co-occurrence weighted masking**: To fix the estimated joint probability distribution that makes the _independence_ assumption, we apply co-occurrence weighted masking to filter out improbable token combinations.

## Instruction Finetuning

We finetune our models a filtered Alpaca dataset. This gives us chat versions of our multi-token models.

<div align="center">
  <img src="{{ site.baseurl }}/assets/img/dynamo-7p3b-t3.gif" alt="DynaMo-7.3B-T3-Chat vs. Pythia-6.9B" width="80%" />
  <br>
  <div align="center" width="100%">
    <em>DynaMo on Pythia-6.9B.</em>
  </div>
  <br>
</div>

## Developer

[Shikhar Tuli](https://github.com/shikhartuli). For any questions, comments or suggestions, please reach me at [stuli@princeton.edu](mailto:stuli@princeton.edu).

## Cite this work

Cite our work using the following bibtex entry:
```bibtex
@article{tuli2023dynamo,
  title={DynaMo: Why Predict Just One Token at a Time?},
  author={Tuli, Shikhar and Lin, Chi-Heng and Hsu, Yen-Chang and Jha, Niraj K, and Shen, Yilin and Jia, Hongxia},
  journal={arXiv preprint arXiv:23XX.XXXXX},
  year={2023}
}
```

## License

We are working with Samsung's legal team to publicly release the source code and model weights. Stay tuned!