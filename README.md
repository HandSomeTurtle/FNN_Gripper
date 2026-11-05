# FNN Gripper

This repository brings together three source repositories and the Gripper
planning adapter. The source repositories are Git submodules, so each keeps its
own history and can also be used independently.

## Contents

- `PlanForge/` — PlanForge fork; PDDL-to-SAS+ translator and planner.
- `fnn-verification/` — FNN verification tools.
- `socs26-repo/` — SoCS26 code and the Gripper experiment at
  `run-experiments/gripper-planforge/`.

## Clone

Clone with submodules so all three source repositories are checked out:

```bash
git clone --recurse-submodules https://github.com/HandSomeTurtle/FNN_Gripper.git
```

For an existing clone, initialize or update its submodules with:

```bash
git submodule update --init --recursive
```

## Gripper PDDL-to-SAS+ and enumeration

Open a WSL/Ubuntu terminal and build both PlanForge command-line programs:

```bash
cd FNN_Gripper
cargo build --release --locked --manifest-path PlanForge/Cargo.toml \
  -p planforge --bin planforge-translator --bin planforge
```

Then run the Gripper pipeline:

```bash
cd socs26-repo/run-experiments/gripper-planforge
python3 pipeline.py prepare
python3 -m unittest discover -s checks -p 'test_*.py' -v
```

See `socs26-repo/run-experiments/gripper-planforge/README.md` for requirements,
configuration, outputs, and test details.

## Updating submodules

Each submodule points to a commit in the corresponding `HandSomeTurtle` fork.
After pushing changes to a fork, update its checkout here and commit the new
submodule pointer in this repository.
