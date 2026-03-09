# Logs

This directory stores local training outputs. Runtime artifacts remain ignored by git, but the documentation in this folder is tracked so people can find the current maintained configurations.

## Maintained Configurations

### Perceptive Shadowing

As of `2026-03-09`, keep the perceptive shadowing configuration notes here, while pretrained weights are distributed separately outside the repository (for example via Google Drive).

- Experiment: `g1_perceptive_shadowing`
- Weight distribution: external link / Google Drive
- Notes policy: keep config details in repo, keep weight files and share links outside repo history unless explicitly requested

### Key Config Snapshot

The exact saved configs for that run are:

- Agent config: `logs/instinct_rl/g1_perceptive_shadowing/2026-03-09_00-35-24/params/agent.yaml`
- Env config: `logs/instinct_rl/g1_perceptive_shadowing/2026-03-09_00-35-24/params/env.yaml`

Useful highlights copied from the saved config:

- Device: `cuda:0`
- Policy: `EncoderActorCritic`
- PPO learning rate: `0.001`
- PPO entropy coef: `0.005`
- Actor / critic hidden dims: `[512, 256, 128]`
- Parallel envs: `3072`
- Decimation: `4`
- Episode length: `10.0 s`
- Motion / terrain dataset: `/home/duanxin/Xyk/Datasets/20251116_50cm_kneeClimbStep1`

### How To Use It

Use the saved config snapshot as the reference when preparing a released checkpoint package:

```bash
sed -n '1,160p' logs/instinct_rl/g1_perceptive_shadowing/2026-03-09_00-35-24/params/agent.yaml
sed -n '1,220p' logs/instinct_rl/g1_perceptive_shadowing/2026-03-09_00-35-24/params/env.yaml
```

If you publish pretrained weights externally, document the share link together with a runnable play command in a task-facing README:

```bash
# Google Drive (fill in when available)
# https://drive.google.com/...
instinct-play Instinct-Perceptive-Shadowing-G1-Play-v0 \
  --load-run <downloaded_run_dir> \
  --checkpoint <checkpoint_file>
```

If a newer configuration becomes the maintained one, update this README together with the task-facing README links.
