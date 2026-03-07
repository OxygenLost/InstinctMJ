# BeyondMimic Task

This directory contains the implementation of the BeyondMimic task, which replicates the training configuration from the BeyondMimic whole body tracking approach (https://github.com/HybridRobotics/whole_body_tracking).

## Structure

```
beyondmimic/
├── __init__.py                    # Main module exports
├── beyondmimic_env_cfg.py        # Base environment configuration
├── cli_args.py                   # Command line interface arguments
├── play.py                       # Script to play trained policies
├── test_integration.py           # Integration test script
├── README.md                     # This file
├── config/                       # Robot-specific configurations
│   ├── __init__.py
│   └── g1/                       # G1 robot configurations
│       ├── __init__.py
│       ├── beyondmimic_plane_cfg.py  # G1 plane environment config
│       └── agents/               # Agent configurations
│           ├── __init__.py
│           └── beyondmimic_ppo_cfg.py  # PPO agent config
└── mdp/                          # MDP components
    ├── __init__.py
    ├── curriculums.py            # Curriculum learning terms
    └── terminations.py           # Termination conditions
```

## Key Features

### BeyondMimic Approach
- **Link-level tracking**: Focuses on tracking individual body links rather than just joint positions
- **Relative world frame**: Uses relative world frame for link position and rotation tracking
- **Gaussian rewards**: Implements Gaussian-based reward functions for smooth tracking
- **Adaptive weighting**: Includes curriculum learning with adaptive motion weighting

### Reward Structure
The BeyondMimic reward system includes:
- Base position imitation (Gaussian)
- Base rotation imitation (Gaussian)
- Link position imitation (Gaussian, relative world frame)
- Link rotation imitation (Gaussian, relative world frame)
- Link linear velocity imitation (Gaussian)
- Link angular velocity imitation (Gaussian)
- Action rate regularization
- Joint limit penalties
- Undesired contact penalties

## Usage

### Training
```python
from instinct_mj.tasks.shadowing.beyondmimic.config.g1.beyondmimic_plane_cfg import G1BeyondMimicPlaneEnvCfg
from instinct_mj.tasks.shadowing.beyondmimic.config.g1.agents.beyondmimic_ppo_cfg import G1BeyondMimicPPORunnerCfg

# Create environment configuration
env_cfg = G1BeyondMimicPlaneEnvCfg()

# Create agent configuration
agent_cfg = G1BeyondMimicPPORunnerCfg()
```

### Playing Trained Policies
```bash
python source/instinct_mj/instinct_mj/tasks/shadowing/beyondmimic/play.py --checkpoint /path/to/checkpoint.pt
```


## Differences from Original BeyondMimic

While following the BeyondMimic approach, this implementation adapts to the current codebase's design patterns:

1. **Configuration Structure**: Uses the existing `@dataclass(kw_only=True)` pattern and configuration hierarchy
2. **MDP Components**: Integrates with existing MDP functions and reward terms
3. **Asset Integration**: Uses the existing G1 robot asset configurations
4. **Motion Reference**: Leverages the existing motion reference system
5. **Monitoring**: Uses the existing monitoring and logging infrastructure

## Motion Data

The configuration is set up to use the Ubisoft LAFAN-1 dataset with GMR retargeting for the G1 robot. Make sure you have the appropriate motion data available at:
```
~/Datasets/UbisoftLAFAN1_GMR_g1_29dof_torsoBase_retargetted_instinctnpz
```

## References

- BeyondMimic: https://github.com/HybridRobotics/whole_body_tracking
- LAFAN-1 Dataset: https://github.com/ubisoft/ubisoft-laforge-animation-dataset
