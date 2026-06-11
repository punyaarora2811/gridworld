# Q-Learning GridWorld

A compact, from-scratch implementation of Q-learning where an agent learns to reach a goal in a 2D grid with randomly generated obstacles. No external RL frameworks—everything is custom built.

## How it works

1. The grid is generated with random obstacles; a BFS check ensures a valid path always exists
2. The Q-table is initialized to zeros
3. Training begins with the agent starting at a fixed start cell, aiming for the goal cell
4. Actions are chosen epsilon-greedily from the Q-table
5. After each step, Q is updated using the TD target with the max over next-state actions
6. Episodes terminate on reaching the goal or hitting a step limit
7. The visualization is updated at each step to reflect learning progress

## Setup

```bash
git clone https://github.com/punyaarora2811/gridworld.git
cd gridworld
pip install -r requirements.txt
```

## Usage

```bash
python main.py
```

A window will open showing a four-panel dashboard with training visualization:
- Current episode trajectory
- Current greedy policy
- Heatmap of max Q-values per state
- Moving average of returns

![Q-Learning GridWorld Demo](media/git.gif)

## Configuration

Adjust hyperparameters by editing `config.yml`:

```yml
environment:
  grid_size: 20
  obstacle_probability: 0.3
  actions: [0, 1, 2, 3]
  action_to_delta: { 0: [0, -1], 1: [1, 0], 2: [0, 1], 3: [-1, 0] } # Up # Right # Down # Left
  step_reward: -5.0
  goal_reward: 500.0
  invalid_move_penalty: -10.0

agent:
  alpha: 0.2
  gamma: 0.995
  epsilon: 1.0
  epsilon_min: 0.002
  epsilon_decay: 0.995

trainer:
  max_steps_per_episode: 200
  reward_avg_window: 100
```

## Project structure

| File | Description |
|---|---|
| `main.py` | Entry point and training loop |
| `src/environment.py` | Grid environment with obstacle generation |
| `src/agent.py` | Q-learning agent implementation |
| `src/trainer.py` | Training orchestration |
| `src/visualizer.py` | PyGame UI and visualization |
| `config.yml` | Hyperparameter configuration |
| `requirements.txt` | Python dependencies |

## Tech stack

- Python, NumPy
- PyGame — real-time visualization with keyboard controls
- PyYAML — configuration management
