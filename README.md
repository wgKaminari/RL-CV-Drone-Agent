# RL CV Drone Agent

A drone agent that learns to fly with **reinforcement learning (RL)** from what it sees through its camera, using **computer vision (CV)**.

## Layout

```
src/drone_agent/
  envs/     simulation environments (Gymnasium-style)
  vision/   camera processing: detection, segmentation, feature encoders
  agents/   RL policies and training loops
configs/    experiment settings
scripts/    training, evaluation and recording entry points
tests/      unit tests
data/       datasets            (not in Git)
models/     trained checkpoints (not in Git)
logs/       training logs       (not in Git)
```

## Setup

```bash
python3 -m venv .venv
.venv/bin/pip install -e .
```

Requires Python 3.12 or newer.
