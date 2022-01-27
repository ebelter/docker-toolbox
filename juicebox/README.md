# View HiC Files with Juicebox on Compute1
Run juicebox on compute1 inside an internet browser with NoVNC!
## Docs 
### Juicebox/Juicer Docs:
https://github.com/aidenlab/Juicebox/wiki
https://github.com/aidenlab/juicer/wiki
### RIS DOCs on NoVNC:
https://docs.ris.wustl.edu/doc/compute/recipes/tools/igv-dockerimage.html
https://docs.ris.wustl.edu/doc/compute/recipes/docker-on-compute.html?highlight=docker%20registry#build-images-using-compute
## Run on Compute1
### Run the Service
* Memory:   add as needed, update juicebox script
* Groups:   whatever compute group you are in
* Volumes:  your $HOME (required) and otehr volumes to view HiC files
* Port:     run on any you'd like
```
$ LSF_DOCKER_PRESERVE_ENVIRONMENT=false LSF_DOCKER_VOLUMES="${HOME}:${HOME} /storage1/fs1/hprc:/storage1/fs1/hprc' LSF_DOCKER_PORTS='8080:8080' bsub -Is -R 'select[port8080=1]' -q general-interactive -G compute-hprc -a 'docker(ebelter/juicebox:compute1)' supervisord -c /app/supervisord.conf
```
### Run Juicebox an Internet Browser
Locate which compute client the service is running on. Note its number  
Direct a browser to this page on the compute client (fill in ### with client number): __https://compute1-exec-###.compute.ris.wustl.edu:8080/vnc.html__  
Click connect, then enter password _hic_  
In the terminal, run __/app/juicebox/scripts/juicebox__  
In _juicebox_, select File -> Open ... navigate to HiC files  
## Build Dockers on Compute1
Update groups and docker tag as needed.
### Dokcer Hub Login
$ LSB_DOCKER_LOGIN_ONLY=1  bsub -G compute-chprc -q general-interactive -Is -a 'docker_build' -- .
### Build!
$ THIS_DOCKER=ebelter/igv:compute1 bsub -G compute-hprc -q general-interactive -Is -a 'docker_build(ebelter/juicebox:compute1)' -- .
