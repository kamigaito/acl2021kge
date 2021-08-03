# Configuration Files

This directory contains configuration files used in our paper.

## Format

The names for each file indicate the following information:

```
{MODEL NAME}-{DATASET NAME}-{LOSS FUNCTION}.yaml
```

Each `{LOSS FUNCTION}` indicates the following loss functions:

- `ns_w_uni`: Negative sampling with uniform noise. 
- `sans`: Self-adversarial negative sampling.
- `ns_w_freq`: Negative sampling with unigram noise. 
- `sce`: Softmax cross-entropy.
- `sce_w_ls`: Softmax cross-entropy with label smoothing.
- `sce_w_bc`: Softmax cross-entropy with backward correction (unigram distribution).
