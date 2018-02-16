# pycortex Singularity container

This repository contains a singularity definition file to create a
container with [pycortex](https://gallantlab.github.io), FreeSurfer, and
FSL. It installs the `glrework-merged` branch of pycortex. Pycortex's
filestore database needs to be mounted externally so that it is
persistent, and must be pointed to `/cortex-filestore` inside the
container.

## How to

### 1. Build the container (this assumes Singularity >= 2.4.2)

```terminal
singularity build pycortex.img Singularity
```

### 2. Run it mounting the relevant directories, e.g.

```terminal
singularity run -B /path/to/my/data:/data \
    -B /path/to/my/filestore:/cortex-filestore \
    -e -c pycortex.img
```

This will start a shell inside the container; then one can run a jupyter
notebook session with

```terminal
jupyter notebook --no-browser --port=9999
```

The container can also be used as a wrapper for commands, for example

```terminal
$ singularity run \
    -B /path/to/my/filestore:/cortex-filestore \
    -e -c pycortex.img \
    "python -c 'import cortex; print(cortex.__file__)'"

/src/pycortex/cortex/__init__.py
```
