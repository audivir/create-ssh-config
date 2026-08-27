# create-ssh-config

Create a SSH config file for multiple hosts and proxyjumps. Hosts are configured with a
YAML file, validated against the schema in `schema.json`.

## Prerequisites

- Python 3.10 or newer.
- A `check-subnet` script on `PATH` if any host uses `check-subnet` (bundled as
  `create_ssh_config/assets/check-subnet`).

## Installation

```shell
pip install git+https://github.com/audivir/create-ssh-config
```

## Usage

```shell
create-ssh-config hosts.yaml
```

Example `hosts.yaml`:

```yaml
- host: host1
  user: user1
  auth: # optional, default: publickey
    - password
    - publickey
  identityfile: "/path/to/identityfile" # optional, default: ~/.ssh/id_ed25519
  hostnames:
    # at least one hostname is required
    # the last hostnames check-subnet must be undefined or null
    # everything else is optional
    # if the check-subnet is "ping" the hostname is used.
    - hostname: host1.example.com # no default
      proxyjump: other host # default: none
      check-subnet:
        ping # default: arguments to check_subnet script
        # if ping, the hostname is used
      port: 1222 # default: 22
      # but everything is optional
```

Run `create-ssh-config --help` for the full list of options.

## License

This project is licensed under the `MIT` license.
