# singularity-openms

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/601)

Receipes for Singularity containers that can run OpenMS (2.2 and 2.3 with thirdparty tools).

These are early builds for testing only. 

The receipes are based on OpenMS docker containers available from the OpenMS team.  For examples checkout 
https://hub.docker.com/u/hroest/

# Usage
## Pull the container to your machine (and optionally name custom, or by hash/commit:

```
singularity pull shub://mafreitas/singularity-openms
singularity pull --name customname.img shub://mafreitas/singularity-openms
singularity pull --commit shub://mafreitas/singularity-openms
singularity pull --hash shub://mafreitas/singularity-openms
```

## Shell into the container:
```
singularity shell shub://mafreitas/singularity-openms
```
## Run the container:
```
singularity run shub://mafreitas/singularity-openms
```
## Build using as a base:
```
sudo singularity build singularity-openms.simg shub://mafreitas/singularity-openms
```

# Containers
Latest & 2.3+ - contain the latest build (2.3.0) and thirdparty tools.  
2.2+ - contains 2.2.0 and thirdparty tools . 
contrib - contains the dependencies and contributing libraries. 
dependencies - contains the base image with all build dependencies.  

To pull a specific container add the appropriate tag.  
For example to pull the 2.2+ container use:

```
singularity pull shub://mafreitas/singularity-openms:2.2+
```
