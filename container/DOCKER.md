# Mini-NDN in [Docker](https://www.docker.com/)

Mini-ndn can be easily installed on Docker and also available with prebuilt image on the [Docker Hub](https://hub.docker.com/).

### `docker build` or `docker pull`
The [Dockerfile](https://github.com/ashiqopu/docker-minindn/blob/master/Dockerfile) can be used directly to `build` an image from scratch.

* Build with `Dockerfile`:
  * Open terminal and use the following command:
    ```bash
    git clone https://github.com/ashiqopu/docker-minindn
    cd docker-minindn
    ```
  * Type and enter.
    ```bash
    docker build -t minindn .
    ```
  * You can then access the container through shell with,
    ```bash
    docker run -m 4g --cpus=4 -it --rm --privileged \
           -v /lib/modules:/lib/modules \
           minindn bin/bash
    ```

* Pull from hub:
  * Open a terminal and type: 
    ```bash
    docker pull marahman/minindn:v0.2
    ```

  * You can then access the container through shell with,
    ```bash
    docker run -m 4g --cpus=4 -it --rm --privileged -e DISPLAY \
              -v /tmp/.X11-unix:/tmp/.X11-unix \
              -v /lib/modules:/lib/modules \
              marahman/minindn:v0.2 bin/bash
    ```

### Notes:
* Memory (-m), CPU (--cpus) are recommended by Mini-NDN.
* `--privileged` is mandatory for underlying [Mininet](http://mininet.org/) to utilize virtual switch
* Root directory on `run` is `/mini-ndn` containing the installation and examples.
* [WIP] There might be error showing up regarding `infoedit` which can be resolved by running `./install -a` (once or twice). We're working on a fix.
* GUI may not work for now due to docker and xterm setup issues and is independent from Mini-NDN.
