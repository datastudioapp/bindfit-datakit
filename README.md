# Bindfit datakit

Bindfit is a binding constant fitting tool designed to work with classical supramolecular titration data obtained from NMR, UV, Fluorescence and other methods.

* 🗒️ [Datakit documentation](https://docs.opendata.studio/)
* 💻 [Bindfit Python library GitHub](https://github.com/opendatastudio/bindfit)

## Usage

Initialise virtualenv and install DataStudio CLI:

```bash
python -m venv .venv
pip install datastudio-cli

# Test it works
ds
```

Ensure you build the Docker container first:

```bash
# Build Bindfit container
cd bindfit/container
./build.sh

# Build python-run-base if not built
# Navigate to python-run-base repository
./build.sh
```

You can now run the datakit:

```bash
cd bindfit-datakit

ds reset                                   # Clear any previous outputs
ds init                                    # Initialise the default run
ds load data ./data/nmr11.csv              # Load input data
ds set model "nmr1to1"                     # Set fit model
ds set method "nelder-mead"                # Set fit method
ds set inputParams.k.init 314              # Set initial parameter guess
ds run                                     # Run algorithm
ds show outputParams                       # View optimised parameters
ds show summary                            # View fit summary
ds view fitGraphMatplotlib                 # View fit graph
```

## Development

### Requirements

* Docker
* Python (to run CLI)
* [opendatastudio/cli](https://github.com/opendatastudio/cli)
* [opendatastudio/containers](https://github.com/opendatastudio/containers)

### Set up pre-commit hooks

Set up included Flake (`flake.nix`) with direnv (`.envrc`) to automatically load development environment.

Install/run pre-commit hooks:
```
pre-commit install
pre-commit run --all-files
```

### Build execution container

Build base execution container:
```
# Navigate to python-run-base repository
./build.sh
```

Build bindfit-datakit container:
```
# Navigate back to bindfit-datakit repository
cd containers
./build.sh
```

### Install CLI

```
python -m venv .venv
source .venv/bin/activate
pip install -e /PATH/TO/CLI

ds  # Check CLI is installed
```

See [Usage](#usage) for command reference.
