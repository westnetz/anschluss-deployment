# anschluss-deployement

This repository contains the glue to setup [anschluss](https://github.com/westnetz/anschluss) on
[CoreOS](https://coreos.com/) using [Ignition](https://coreos.com/ignition/docs/latest/).

## Usage

Generate the ingition config. This requires docker to be usable locally:

```
cd ignition
make config
```

Spawn a machine. This example assumes Digital Ocean:

```
doctl compute droplet create anschluss.example.com \
    --size s-1vcpu-1gb \
    --region fra1 \
    --image coreos-stable \
    --ssh-keys your-key-id \
    --user-data-file config.json
```

You need to ensure that `anschluss.example.com` resolves to the IP of the machine
you just started.
