# ghcr

Steps I followed for the `ubuntu-mongo` image:

1. Start Docker by `systemctl start docker` or the desktop application.
2. Login to _ghcr_ by:
    1. `export CR_PAT=YOUR_KEY && gh_un=YOUR_GITHUB_USERNAME && cn=CONTAINER_NAME`
    2. `echo $CR_PAT | docker login ghcr.io -u $gh_un --password-stdin`
3. Change working directory to the folder with your _Dockerfile_.
3. `docker build -t ghcr.io/$gh_un/$cn .`
4. `docker push ghcr.io/$gh_un/$cn:latest`

After these steps, you can load the image in a server with [Slurm Workload Manager](https://slurm.schedmd.com) and its plugin named [Pyxis](https://github.com/NVIDIA/pyxis) installed by the command `srun --container-image ghcr.io\#$gh_un/$cn:latest --pty bash`.
