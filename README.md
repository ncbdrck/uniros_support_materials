# Support Materials for the UniROS Framework

This repository is the entry-point pointer for users who arrive from
the UniROS paper. It lists the working code repositories, the install
paths, and the documentation site. All of the actual code lives in
the linked repositories — this repo is documentation only.

**Paper**: Kapukotuwa, J., Lee, B., Devine, D., Qiao, Y. (2025).
*UniROS: ROS-Based Reinforcement Learning Across Simulated and
Real-World Robotics.* Sensors, 25(18), 5679.
[doi.org/10.3390/s25185679](https://doi.org/10.3390/s25185679)

**Full documentation**: [uniros.readthedocs.io](https://uniros.readthedocs.io/)


## What's in the UniROS ecosystem

The framework is split into **four core packages** plus
**two application packages** that ship pre-built environments and
training scripts.

### Core framework

| Repo | Role |
|---|---|
| [UniROS](https://github.com/ncbdrck/UniROS) | Unified abstraction layer; hosts the multiprocessing gym-env proxy. Bundles MultiROS + RealROS as submodules. |
| [MultiROS](https://github.com/ncbdrck/multiros) | Gazebo-based simulation environments. |
| [RealROS](https://github.com/ncbdrck/realros) | Real-hardware counterpart to MultiROS. Same gym API, talks to physical robots. |
| [sb3_ros_support](https://github.com/ncbdrck/sb3_ros_support) | Stable Baselines 3 algorithm wrappers (PPO, A2C, DDPG, TD3, SAC, DQN, plus goal-conditioned variants) configured for ROS. |

### Applications

| Repo | Role |
|---|---|
| [rl_environments](https://github.com/ncbdrck/rl_environments) | Pre-built `gymnasium` environments. Currently covers RX200, Ned2, VX300S, UR5e — 54 registered env IDs (48 core task envs plus extra Kinect/ZED2 sensor variants for RX200) across reach / push / pick-and-place tasks, both sim and real. |
| [rl_training_validation](https://github.com/ncbdrck/rl_training_validation) | Working training and validation scripts for the pre-built envs. Includes a multi-task training script that trains jointly across sim and real. |
| [vx300s_mujoco_envs](https://github.com/ncbdrck/vx300s_mujoco_envs) | Experimental ViperX-300 S environments on the in-progress MuJoCo backend (`mujoco_ros_pkgs`). Validates the MuJoCo backend end-to-end on reach / push / pick-and-place (plus goal-conditioned variants). |

### Per-robot description-extras helpers

| Repo | Role |
|---|---|
| [reactorx200_description](https://github.com/ncbdrck/reactorx200_description) | RX200 URDF wrap, table, cube, sensor mounts. |
| [niryo_ned2_description_extras](https://github.com/ncbdrck/niryo_ned2_description_extras) | Ned2 URDF wrap + Kinect v2 + adaptive-gripper variant. |
| [viperx300s_description](https://github.com/ncbdrck/viperx300s_description) | VX300S URDF wrap + Kinect + control config. |
| [ur5e_description_extras](https://github.com/ncbdrck/ur5e_description_extras) | UR5e + Robotiq 2F-85 URDF wrap, base stand, cafe-table scene, controllers. |
| [common-sensors](https://github.com/ncbdrck/common-sensors) | Shared sensor models (Kinect v2, ZED 2, RealSense D405). |

### Real-side cube tracker

| Repo | Role |
|---|---|
| [rl_envs_cube_tracker](https://github.com/ncbdrck/rl_envs_cube_tracker) | AprilTag-based `/cube_pose` publisher used by real push / pick-and-place envs. Per-camera-per-robot extrinsic YAMLs ship for Kinect v2, ZED 2, and D405. |


## Install

The fastest path is the bootstrap installer, which installs ROS
Noetic, all four framework packages, both application packages,
the robot vendor packages, the description-extras helpers, the
cube tracker, and the RealSense D405 SDK in one go:

```bash
git clone -b gymnasium https://github.com/ncbdrck/UniROS.git /tmp/uniros_bootstrap
bash /tmp/uniros_bootstrap/install_uniros_stack.sh -y -p ~/uniros_ws
```

Identical copies of the installer ship in every ecosystem repo, so
you can run it from whichever one you cloned first.

**Don't have Ubuntu 20.04?** The same stack is available as a Docker
image (Ubuntu 22.04 / 24.04 hosts, WSL2, machines with GPUs whose
drivers have no Ubuntu 20.04 support):

```bash
cd /tmp/uniros_bootstrap/docker
./build.sh
./run_gui.sh    # Gazebo + RViz on host display via rocker
```

See [the install guide](https://uniros.readthedocs.io/en/latest/guides/install.html)
and the [dedicated Docker page](https://uniros.readthedocs.io/en/latest/guides/docker.html)
for the full reference.


## Legacy: OpenAI Gym era

Before the framework was ported to Gymnasium, the working
environments lived in
[reactorx200_ros_reacher](https://github.com/ncbdrck/reactorx200_ros_reacher).
That repo and the `openai_gym` branches of UniROS, MultiROS,
RealROS, and sb3_ros_support are **no longer actively maintained**
and are kept available for reproducibility of the older OpenAI Gym
results only. New work should use the Gymnasium-era stack listed
above.

To run the legacy OpenAI Gym envs:

```bash
cd ~/catkin_ws/src
git clone https://github.com/ncbdrck/reactorx200_ros_reacher.git
```

Then `git checkout openai_gym` in UniROS, MultiROS, RealROS, and
sb3_ros_support, and follow the install instructions in
`reactorx200_ros_reacher`.


## Status

- **Sim envs**: registered and configured in Gazebo across all four
  robots and three tasks. The RX200 reach path is the most-exercised
  end-to-end; the other (robot × task) combinations are in the testing
  queue.
- **Real envs**: registered; hardware validation in progress (the
  RX200 reach path is the most-exercised; the others are in the
  testing queue).
- **Experimental MuJoCo backend**: a parallel MuJoCo backend for
  MultiROS is in active development (not yet in a stable release),
  with `vx300s_mujoco_envs` as the worked example. See the UniROS
  MuJoCo backend guide for install steps.
- **Documentation**: Sphinx + Read the Docs at
  [uniros.readthedocs.io](https://uniros.readthedocs.io/), including
  per-env reference pages following the Gymnasium-Robotics layout.

## Roadmap

- Complete real-hardware validation for VX300S, Ned2, and UR5e
  across push and pick-and-place tasks.
- Remote-env mode for the Docker image (env in container, learner
  on host) so users on modern Python / CUDA can train against the
  pinned ROS Noetic stack. See the Docker docs page for status.
- ROS 2 port. Long-term; current framework targets ROS Noetic.
