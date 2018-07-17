### Docker image for MaxBin 2

An optimized Docker image for running MaxBin2

#### Usage instructions

Set a workspace path (e.g the directory where the contigs and abundances are located) 
and mount it on the Docker container while running the image.

```bash
BASE=/path/to/local/workspace/
docker run --rm --volume ${BASE}:${BASE} omixer/maxbin:2.2.5 (MaxBin ARGS)
```

For examples please check the [official image](https://hub.docker.com/r/karlon27/maxbin/)