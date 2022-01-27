Juice Box on compute1, view in a browser via noVNC >>

<<< DOCS >>>

Juice Box, Juicer Docs:
https://github.com/aidenlab/Juicebox/wiki
https://github.com/aidenlab/juicer/wiki

RIS DOCs on NoVNC:
https://docs.ris.wustl.edu/doc/compute/recipes/tools/igv-dockerimage.html
https://docs.ris.wustl.edu/doc/compute/recipes/docker-on-compute.html?highlight=docker%20registry#build-images-using-compute

<<< BUILD ON COMPUTE1 >>

# Update groups and tags as needed.

< LOGIN >
$ LSB_DOCKER_LOGIN_ONLY=1  bsub -G compute-chprc -q general-interactive -Is -a 'docker_build' -- .

< BUILD >
$ THIS_DOCKER=ebelter/igv:compute1 bsub -G compute-hprc -q general-interactive -Is -a 'docker_build(ebelter/juicebox:compute1)' -- .

<<< RUN >>>

< SERVER >

# Memory:   add as needed, update juicebox script
# Groups:   whatever compute group you are in
# Volumes:  your $HOME (required) and otehr volumes to view HiC files
# Port:     run on any you'd like

$ LSF_DOCKER_PRESERVE_ENVIRONMENT=false LSF_DOCKER_VOLUMES="${HOME}:${HOME} /storage1/fs1/hprc:/storage1/fs1/hprc' LSF_DOCKER_PORTS='8080:8080' bsub -Is -R 'select[port8080=1]' -q general-interactive -G compute-hprc -a 'docker(ebelter/juicebox:compute1)' supervisord -c /app/supervisord.conf

< RUN APP >

Direct a browser to this page on the compute client: https://compute1-exec-###.compute.ris.wustl.edu:8080/vnc.html
Click connect, enter password "hic"
In the terminal, run "/app/juicebox/scripts/juicebox"

