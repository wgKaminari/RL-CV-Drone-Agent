# RL CV Drone Agent

**Autonomous drone control with deep reinforcement learning and computer vision.**

RL CV Drone Agent is a research and engineering project that trains an autonomous quadcopter agent to perceive its surroundings through an onboard camera and make flight decisions end to end. Visual perception (object detection, segmentation and learned feature encoders) is combined with deep reinforcement learning policies, so the agent learns behaviour such as navigation, obstacle avoidance and target tracking from experience in simulation, rather than from hand-written rules.

> **Status:** early development. The project structure is in place; environments, perception and training pipelines are being built. See the [roadmap](#roadmap).

## Objectives

- **Vision-based control:** learn flight policies directly from camera observations, with optional state inputs (position, velocity, attitude).
- **Modular perception:** interchangeable vision back-ends, from raw-pixel CNN encoders to pretrained detectors and segmenters, so their effect on learning can be compared.
- **Simulation first:** train and evaluate safely and reproducibly in physics-based drone simulators before any real-world deployment.
- **Reproducible experiments:** every run is defined by a configuration file, with fixed seeds, logged metrics and versioned checkpoints.
- **Sim-to-real readiness:** domain randomisation and a clean separation between policy and hardware interface, to ease future transfer to physical drones.

## Planned tasks

| Task | Description |
|---|---|
| Hover and waypoint flight | Stabilise and reach target positions under disturbances |
| Obstacle avoidance | Navigate cluttered environments using vision only |
| Target tracking | Detect, follow and keep a moving object in frame |
| Visual navigation | Reach goals specified by images or landmarks |

## Architecture

```
          ┌──────────────┐     ┌───────────────────┐     ┌──────────────┐
 camera ─▶│   vision/    │────▶│     agents/       │────▶│    envs/     │
 frames   │  perception  │     │  RL policy (PPO,  │     │  simulator / │
          │  & encoders  │     │  SAC, …)          │     │  drone API   │
          └──────────────┘     └───────────────────┘     └──────┬───────┘
                 ▲                                              │
                 └──────────── observations, rewards ◀──────────┘
```

| Module | Responsibility |
|---|---|
| `src/drone_agent/envs/` | Gymnasium-compatible drone environments: observations, actions, rewards, episode logic |
| `src/drone_agent/vision/` | Image preprocessing, detection, segmentation and feature encoders |
| `src/drone_agent/agents/` | RL algorithms, policy networks, training and evaluation loops |
| `configs/` | Experiment configurations (environment, model, hyperparameters) |
| `scripts/` | Entry points for training, evaluation and recording flights |
| `tests/` | Unit and integration tests |

Datasets (`data/`), trained models (`models/`) and training logs (`logs/`) are kept out of version control.

## Getting started

Requirements: Python 3.12 or newer, Linux recommended; a CUDA-capable GPU is recommended for training.

```bash
git clone https://github.com/wgKaminari/RL-CV-Drone-Agent.git
cd RL-CV-Drone-Agent
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

Training and evaluation commands will be documented here as the pipelines are added.

## Roadmap

- [x] Project structure and packaging
- [ ] Simulation environment integration and a Gymnasium wrapper
- [ ] Baseline RL agent on state observations (hover, waypoints)
- [ ] Vision pipeline: camera observations and CNN encoder
- [ ] Vision-based policies for obstacle avoidance
- [ ] Pretrained detector integration for target tracking
- [ ] Experiment tracking, evaluation benchmarks and flight recordings
- [ ] Domain randomisation for sim-to-real transfer

## Contributing

This is currently a personal research project. Issues with ideas, questions or bug reports are welcome.

## License

No license has been chosen yet; all rights are reserved until one is added.
