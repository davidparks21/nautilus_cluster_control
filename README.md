# nautilus_cluster_control
Scripts for running processes on the Nautilus cluster

Examples:

```
# 0 GPUs, 4 CPU cores, 4GB RAM default
narun python mymodel.py

# All options
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
navolume create myvolumename 100GB
navolume sync source_local_path destination_container_path
navolume list
navolume delete myvolumename

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


