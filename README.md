# ghcr

Steps I followed for the `ubuntu-mongo` image:

1. Start Docker by `systemctl start docker` or the desktop application.
2. Login to _ghcr_ by:
    1. `export CR_PAT=YOUR_KEY`
    2. `echo $CR_PAT | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin`
3. Change working directory to the folder with your _Dockerfile_.
3. `docker build -t ghcr.io/furkanakkurt1335/ubuntu-mongo .`
4. `docker push ghcr.io/furkanakkurt1335/ubuntu-mongo:latest`

After these steps, you can load the image in a server with [Slurm Workload Manager](https://slurm.schedmd.com) and its plugin named [Pyxis](https://github.com/NVIDIA/pyxis) installed by the command `srun --container-image ghcr.io\#furkanakkurt1335/ubuntu-mongo:latest --pty bash`.
