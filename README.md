# Drupal CI Puppet

This repo provides several pieces that work together to configure a machine
suitable to run a Drupal site.

Pieces are some Puppet stuff, a Vagrantfile and scripts to make it run (without
a Puppet master).

## Set up

Prepare the system to run Puppet:

```
./standalone/install
```

Apply the Puppet configuration:

```
./standalone/apply
```

## Vagrant

A Vagrantfile is provided for convenience. It is ready to bring up a machine and
provision it with Puppet.

Along the Vagrantfile, a facility to tweak the box configuration is provided.
It is based on a yaml file and is useful to avoid touching the Vagrantfile.

```
cp Vagrantfile-config.yaml.example Vagrantfile-config.yaml
vi Vagrantfile-config.yaml
```

## Repo contents

- `Puppetfile`: File to declare Puppet modules used.
- `hieradata` : Modules' configuration data.
- `files`     : Puppet static files.
- `manifests` : Puppet entry point. It is almost empty because all configuration is data driven.
- `standalone`: Scripts and obscure stuff to make Puppet work without a master.
- `Vagrant*`  : Vagrantfile and configuration data.

## Compatibility

Right now it only works on Debian and derivatives. CentOS support is ongoing.

