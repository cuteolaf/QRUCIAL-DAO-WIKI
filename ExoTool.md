## Prerequisites

- docker
- docker compose (?)
    - might be useful to have this too, would remove user error.

## Installation

1.  git clone the repo `https://github.com/Qrucial/QRUCIAL-DAO.git`
2.  cd into `./QRUCIAL-DAO/exotools/` directory
3.  run the command `docker build -t exotools ./dockerfiles/`
    - this builds the image based on the instructions in the dockerfile at `./dockerfiles/`
4.  make the local audit dir `mkdir auditdir`
    - this directory is the shared point between the docker and your file system.
5.  run the command `docker run --name=auditor -v $(pwd)/auditdir:/auditdir exotools`
    - Run a container named "auditor" based on the image exotools.
    - mount the local folder "auditdir" to the remote folder "/auditdir"
6.  to run it again use the command `docker start -a auditor`
    - this runs the same script and shows the output in the terminal
7.  to execute specific commands run `docker exec <...>`

* * *

## Experimental ideas

- if we want to run many of these containers in parallel we might have to worry about performance at some point. i believe that using `docker <pause/unpause>` would be the best solution *as far as i know*
    - but to do this we would have to have some sort of scheduler that monitors resource usage and pauses/ unpauses accordingly
- Make each started container have a unique hash based on the current thing that needs to be audited.
    - this would allow us to easily run many in parallel and see what container is working on what file.
    - something like: `XTPATH=audit_files/"$HASH""_$(date +%s)"`
        - where HASH = a 512sha hash of the file.