# anschluss-deployement

This repository contains the glue to setup [anschluss](https://github.com/westnetz/anschluss) on
[CoreOS](https://coreos.com/) using [Ignition](https://coreos.com/ignition/docs/latest/).

## Usage

First, unlock the repository with [git-crypt](https://github.com/AGWA/git-crypt).

```console
git-crypt unlock
```

Then, generate the ingition config. This requires docker to be usable locally:

```console
make -C ignition config
```

Finally, spawn a machine. This example uses Digital Ocean:

```console
doctl compute droplet create anschluss.example.com \
    --size s-1vcpu-1gb \
    --region fra1 \
    --image coreos-stable \
    --ssh-keys your-key-id \
    --user-data-file ignition/config.json
```

You need to ensure that `anschluss.example.com` resolves to the IP of the machine
you just started.

Once the machine has booted completely, anschluss should be up and running.
