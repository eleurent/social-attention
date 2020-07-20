## Abstract

We study the design of learning architectures for behavioural planning in a dense traffic setting. Such architectures should deal with a varying number of nearby vehicles, be invariant to the ordering chosen to describe them, while staying accurate and compact. We observe that the two most popular representations in the literature do not fit these criteria, and perform badly on an complex negotiation task. We propose an attention-based architecture that satisfies all these properties and explicitly accounts for the existing interactions between the traffic participants. We show that this architecture leads to significant performance gains, and is able to capture interactions patterns that can be visualized and qualitatively interpreted.

## Videos

*(Only supported on the [github page](https://eleurent.github.io/social-attention/))*

### Full episode
<p align="center"><video src="assets/1_episode.mp4" width="600" height="600" controls preload></video></p>

### Attention and distance to vehicles
<p align="center"><video src="assets/2_distance.mp4" width="600" height="600" controls preload></video></p>

### Sensitivity to vehicles states
<p align="center"><video src="assets/3_sensitivity.mp4" width="600" height="600" controls preload></video></p>

### Effect of road priorities
<p align="center"><video src="assets/4_priority1.mp4" width="600" height="600" controls preload></video></p>
<p align="center"><video src="assets/4_priority2.mp4" width="600" height="600" controls preload></video></p>

### Supplementary videos
<p align="center"><video src="assets/right.mp4" width="600" height="600" controls preload></video></p>
<p align="center"><video src="assets/straight.mp4" width="600" height="600" controls preload></video></p>

## Reproduce the experiments [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/eleurent/highway-env/blob/master/scripts/intersection_social_dqn.ipynb)

1. Install the [highway-env](https://github.com/eleurent/highway-env) environment

`pip install --user git+https://github.com/eleurent/highway-env`

2. Install the [rl-agents](https://github.com/eleurent/rl-agents) implementations, and clone the repository.

`pip install --user git+https://github.com/eleurent/rl-agents`

3. Train the agents
(repeat for several seeds)

`cd <path/to/rl-agents>/scripts`

* MLP/List

```shell
python experiments.py evaluate configs/IntersectionEnv/env.json \
                               configs/IntersectionEnv/agents/DQNAgent/baseline.json \
                               --train --episodes=4000 --name-from-config
```

* CNN/Grid

```shell
python experiments.py evaluate configs/IntersectionEnv/env_grid_dense.json \
                               configs/IntersectionEnv/agents/DQNAgent/grid_convnet.json \
                               --train --episodes=4000 --name-from-config
```

* Ego-Attention

```shell
python experiments.py evaluate configs/IntersectionEnv/env.json \
                               configs/IntersectionEnv/agents/DQNAgent/ego_attention_2h.json \
                               --train --episodes=4000 --name-from-config
```

4. Visualize the results

`tensorboard --logdir out/IntersectionEnv`

or
`python analyze.py run out/IntersectionEnv/DQNAgent/`
