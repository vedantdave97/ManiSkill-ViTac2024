
# [ManiSkill-Vitac Challenge 2024](https://ai-workshops.github.io/maniskill-vitac-challenge-2024/)

**Table of Contents**

- [Update News](#update)
- [Installation](#installation)
- [Training Example](#example)
- [Submission](#submission)
- [Leaderboard](#leaderboard)
- [Real Robot Evaluation](#real-robot-evaluation)
- [Contact](#contact)
- [Citation](#citation)

## Update
**2024/02/08** Add `render_rgb` option for tactile sensor observations

**2024/02/21** Add multi-gpu to the environment. Now the training script will automatically select multiple gpus when `parallel` in the configuration file is larger than 1.


## Installation

**Requirements:**

- Python 3.8.x-3.11.x
- GCC 7.2 upwards (Linux)
- CUDA Toolkit 11.8 or higher
- Git LFS installed (https://git-lfs.github.com/)


Clone this repo with

```bash
git clone https://github.com/callmeray/ManiSkill-ViTac2024.git
```

Run

```bash
conda env create -f environment.yaml
conda activate mani_vitac
```
**Cuda**

Install Cuda version>11.8. If you have Nvidia 545 drivers, then its Cuda 12.3, or if its Nvidia 535 drivers, then its Cuda 12.2 and so on.
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.3.2/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.2-545.23.08-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.2-545.23.08-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
```
Then add it to your path
```
export PATH=/usr/local/cuda-12.3/bin:$PATH
```

Then use the following commands to install [SapienIPC](https://github.com/Rabbit-Hu/sapienipc-exp), following the [README](https://github.com/Rabbit-Hu/sapienipc-exp/blob/main/README.md) file in that repo.

Make a new soft link for libstd
```
sudo ln -sf /usr/lib/x86_64-linux-gnu/libstdc++.6.0.30 ~/anaconda3/envs/mani_vitac/lib/libstdc++.so.6
```

## Training Example

To train our example policy, run

```bash
# example policy for peg insertion
python scripts/universal_training_script.py --cfg configs/parameters/peg_insertion.yaml
# example policy for open lock
python scripts/universal_training_script.py --cfg configs/parameters/long_open_lock.yaml
```

## Submission 
For policy evaluation in simulation, run

```bash
# evaluation of peg insertion and lock opening
# replace the key and the policy model
python scripts/peg_insertion_sim_evaluation.py
python scripts/open_lock_sim_evaluation.py
```
Submit the evaluation logs by emailing them to [maniskill.vitac@gmail.com](maniskill.vitac@gmail.com)

## Leaderboard

The leaderboard for this challenge is available at [Google Drive](https://docs.google.com/spreadsheets/d/1ZCNSbctm5eyr4Q59KmVBE0ZMo5mt63emFLihbJn1maw/).

## Real Robot Evaluation
Real robot evaluation code demo is contained in `real_env_demo/`. The GelsightMini sensor code is maintained at [GitHub/gelsight_mini_ros](https://github.com/RVSATHU/gelsight_mini_ros/).

## Contact

Join our [discord](https://discord.gg/B8qEVTav) to contact us. You may also email us at [maniskill.vitac@gmail.com](maniskill.vitac@gmail.com)


## Citation

```
@ARTICLE{chen2024tactilesim2real,
              author={Chen, Weihang and Xu, Jing and Xiang, Fanbo and Yuan, Xiaodi and Su, Hao and Chen, Rui},
              journal={IEEE Transactions on Robotics}, 
              title={General-Purpose Sim2Real Protocol for Learning Contact-Rich Manipulation With Marker-Based Visuotactile Sensors}, 
              year={2024},
              volume={},
              number={},
              pages={1-18},
              doi={10.1109/TRO.2024.3352969}}
```

