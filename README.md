# Support Materials for the UniROS Framework

This repository contains the support materials for the `UniROS` framework which includes the following:
- Simulation environments - Made with [MultiROS](https://github.com/ncbdrck/multiros) 
- Corresponding Real-world environments - Made with [RealROS](https://github.com/ncbdrck/realros)
- Stable Baselines3 Support for the ROS-based environments - Made with [SB3_ROS_Support](https://github.com/ncbdrck/sb3_ros_support)

Since the `UniROS` which contains the `MultiROS` and `RealROS` repositories support both `OpenAI Gym `and  `Gymnasium`, the support materials are also made to be compatible with them.

For the installation and usage of the `UniROS` framework, please refer to the [UniROS](https://github.com/ncbdrck/UniROS) repository.

## OpenAI Gym Supported Resources

All the Simulated and Real-world environments made to be compatible with the `OpenAI Gym` interface can be found in the [reactorx200_ros_reacher](https://github.com/ncbdrck/reactorx200_ros_reacher) repository:

### Installation

```bash
cd ~/catkin_ws/src
git clone https://github.com/ncbdrck/reactorx200_ros_reacher.git
```
**Note:** 
- Make sure to follow the installation instructions in the [reactorx200_ros_reacher](https://github.com/ncbdrck/reactorx200_ros_reacher) repository to install the required dependencies.

- Make sure to use `git checkout` the `openai_gym` branch in `UniROS`, `MultiROS`, `RealROS`, and `SB3_ROS_Support` repositories to use run these environments.


## Gymnasium Supported Resources

All the Simulated and Real-world environments made to be compatible with the `Gymnasium` interface can be found in the [rl_environments](https://github.com/ncbdrck/rl_environments) repository:

### Installation

```bash
cd ~/catkin_ws/src
git clone https://github.com/ncbdrck/rl_environments.git
git clone https://github.com/ncbdrck/rl_training_validation.git
```

**Note:**
- Make sure to follow the installation instructions in the [rl_environments](https://github.com/ncbdrck/rl_environments.git) repository to install the required dependencies.
- Make sure to use `git checkout` the `gymnasium` branch in `UniROS`, `MultiROS`, `RealROS`, and `SB3_ROS_Support` repositories to use run these environments.
- Currently, this repository is under development and will be updated soon.


# To-Do
- [ ] Add the installation instructions for the `rl_environments` and `rl_training_validation`repositories.
- [ ] implement more tasks environments for the `Gymnasium` interface.
- [ ] Add support for ROS2.