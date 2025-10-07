# GLADDEST

This repo contains code to train and evaluate the GLADDEST model with Hydra configs.



## Train


### Example: Tox21_MMP (train)

Ensure `general.test_only: null` (default) in `configs/general/general_default.yaml`, then run:

```bash
PYTHONPATH=. python src/main.py +experiment=Tox21_MMP dataset=Tox21_MMP
```

### Example: Tox21_MMP (test)

Set `general.test_only` to the provided checkpoint path, then run the transition-based evaluation:

Option A (edit config):

1) Edit `configs/general/general_default.yaml`:

```yaml
general:
	# ... other fields
	test_only: checkpoints/graph-tf-model/epoch=999.ckpt  # <- put the provided ckpt path here
```

2) Run:

```bash
PYTHONPATH=. python src/transition_method.py +experiment=Tox21_MMP dataset=Tox21_MMP
```

Option B (without editing config):

```bash
PYTHONPATH=. python src/transition_method.py +experiment=Tox21_MMP dataset=Tox21_MMP \
	general.test_only=checkpoints/graph-tf-model/epoch=999.ckpt
```

## Provided checkpoint (example)

We provide a checkpoint for `Tox21_MMP` testing. Use one of the test-only methods above to point `general.test_only` to the file (either via `CKPT_PATH` or a relative path under `checkpoints/`).

##  Transition-method evaluation

There is an evaluation script that computes anomaly scores over a time-interpolation process:

```bash
PYTHONPATH=. python src/transition_method.py +experiment=Tox21_MMP dataset=Tox21_MMP \
	general.test_only=checkpoints/graph-tf-model/epoch=999.ckpt
```

