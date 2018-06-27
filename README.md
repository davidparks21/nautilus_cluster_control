## About
This is a set of scripts designed for developing code that executes
long running tasks on the nautilus cluster, with deep learning and other
ML related tasks which require large dataset to be stored on the
cluster and a dev environment (working on a model for example)
which changes often.

## Installation and prerequisites
TODO

## Workflow

1. Create a yaml file which contains your personal nautilus login
   information and points to a docker image to launch.
    - Default yaml files are provided in the `yaml` directory,
      you will typically start with one of these and edit the
      login information to personalize it.
2. Create a personal volume claim using the `navolume` script.
    - This will create a storage area where your large static files
      can be stored, such as datasets.
    - In the yaml configuration file you will define any directories
      you want to have synced with your personal volume claim each
      time you execute a process on the cluster. This sync will be
      done efficiently (akin to `rsync`) and automatically.
3. Run any process on the cluster using `narun <your command>`
4. If you are disconnected from the server while your process runs
   you can use naconnect to list sessions that are running and reconnect
   to them.

## Examples:

```
# 0 GPUs, 4 CPU cores, 4GB RAM default
narun python mymodel.py

# All options demoed
narun \
   --yaml path_to_yaml_file \
   --gpu 2 \
   --cpu 8 \
   --mem 12GB \
   --sync source_local_path destination_container_path \
   --sync 2nd_source 2nd_destination \
   --volume volume_name \
   -- \
   python mymodel.py

# Managing volumes
navolume create volume_name 100GB
navolume sync volume_name source_local_path destination_container_path
navolume list
navolume delete volume_name

# Connect / reconnect to containers
naconnect list
naconnect getlog container_name
naconnect reconnect container_name

Environment Variables:
	NAUTILUS_YAML
	NAUTILUS_GPUS
	NAUTILUS_CPUS
	NAUTILUS_MEM
	NAUTLIUS_SYNC
	NAUTILUS_VOLUME

Example Usage:

  # Creates the container defined in my.yaml and keeps the local directory
  # ./src synced with the remote directory /home/usr/project/src
  narun --yaml ./my.yaml --sync ./src /home/user/project/src -- myscript.py


```

## Creating your own custom image
TODO

## Prerequisites:
- TODO

## Reference information:

- Logging into nautilus: https://nautilus.optiputer.net/auth
- Rocket chat support forum: https://rocket.nautilus.optiputer.net/



