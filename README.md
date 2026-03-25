The Kiso repository is a template that can be used to start a new Kiso experiment running on FABRIC. The repository defines the directory structure, best practices, etc. to be used while developing an experiment in Kiso.

# Getting Started

## Prerequisites

1. A FABRIC account — sign up at [portal.fabric-testbed.net](https://portal.fabric-testbed.net)
2. [An active FABRIC project allocation](https://learn.fabric-testbed.net/knowledge-base/creating-or-joining-a-project/) — create a new project or join an existing one
3. [SSH keys generated and configured](https://learn.fabric-testbed.net/knowledge-base/generating-ssh-configuration-and-ssh-keys/) — required for Kiso to connect to provisioned nodes over SSH
4. [A FABRIC API token generated](https://learn.fabric-testbed.net/knowledge-base/obtaining-and-using-fabric-api-tokens/) — required for the RC file
5. A FABRIC RC file (used as `rc_file` in the config)
   ```sh
   export FABRIC_BASTION_HOST=bastion.fabric-testbed.net
   export FABRIC_PROJECT_ID=<fabric-project-id>
   export FABRIC_BASTION_USERNAME=<fabric-bastion-username>
   export FABRIC_BASTION_KEY_LOCATION=<path-to-fabric-bastion-key>
   export FABRIC_SLICE_PRIVATE_KEY_FILE=<path-to-fabric-sliver-key>
   export FABRIC_SLICE_PUBLIC_KEY_FILE=<path-to-fabric-bastion-public-key>
   export FABRIC_LOG_LEVEL=INFO
   export FABRIC_LOG_FILE=/tmp/fablib/fablib.log
   export FABRIC_TOKEN_LOCATION=<path-to-fabric-token>
   ```
6. [Permissions requested](https://learn.fabric-testbed.net/knowledge-base/fabric-user-roles-and-project-permissions/) for any resources your experiment requires (GPUs, public IPs, NVMe storage, etc.)
7. Kiso installed: `pip install kiso[fabric]`
8. **(macOS only, optional)** `rsync` from Homebrew: some FABRIC sites assign IPv6 addresses as the management IP, and macOS's built-in `rsync` fails to connect to IPv6 addresses via jump hosts. Install the Homebrew version to fix this:

   ```bash
   brew install rsync
   ```

## Defining the experiment

Define your experiments and the resources it needs in a YAML file named `experiment.yml`.

## Running the experiment

Place any required credentials files in the `secrets` directory. These credentials are referenced in the experiment configuration YAML file.

Place any required config files in the `config` directory.

Place any required data files in the `data` directory.

```sh
# Check Kiso experiment configuration
kiso check experiment-shell.yml

# Provision and setup the resources
kiso up experiment-shell.yml

# Run the experiments defined in the experiment configuration YAML file
kiso run experiment-shell.yml

# Destroy the provisioned resources
kiso down experiment-shell.yml
```

# Versioning

```sh
pip install commitizen

# Committing changes
# Use git cz c or cz c to commit changes

# Tagging a new version, updating the changelog
cz bump
git push --tags

# Use GitHub CLI to create a new release
# gh release create --repo <user-or-org>/<repo> <tag-name>
```

# References

- [Pegasus Workflow Management System](https://pegasus.isi.edu)
- [EnOSlib](https://discovery.gitlabpages.inria.fr/enoslib/)
- [FABRIC](https://portal.fabric-testbed.net)

# Acknowledgements

Kiso is funded by National Science Foundation (NSF) under award [2403051](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2403051).
