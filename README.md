## CVMFS everywhere
Recipe for an ubuntu-based docker container with a working cvmfs client.<br>
Must be run in privileged mode (`docker run --privileged`).

Pre-built images are available on DockerHub at [bluehood/cvmfs_everywhere](https://hub.docker.com/r/bluehood/cvmfs_everywhere).<br>
Try them out with `docker run --privileged -it --rm bluehood/cvmfs_everywhere[:cern]`.

### Example usage
```
root@laptop# docker build .
   ...
   Successfully built 20b4e96d10e8
root@laptop# docker run --privileged -it --rm 20b4e96d10e8
   * Starting automount...                                                 [ OK ] 
   Probing /cvmfs/sft.cern.ch... OK
root@acf3358da5b0:/# ls /cvmfs/sft.cern.ch/lcg/
   app/              dev/              external/         lastUpdate        nightlies/        releases/         
   contrib/          etc/              hepsoft/          mapfile.txt       pkgs_view_ml_1.0  views/  
```

### Usage from inside CERN
For usage from inside the CERN network, the `Dockerfile` must be edited to change
```
CVMFS_HTTP_PROXY=DIRECT
```
to
```
CVMFS_HTTP_PROXY=http://ca-proxy.cern.ch:3128
```

### Changing CVMFS repositories
By default, only the `sft.cern.ch` repository is enabled.
The line in the `Dockerfile` that lists `CVMFS_REPOSITORIES` can be edited to change the list of enabled repos.
