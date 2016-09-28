## Getting started with Docker

* The `docker run` command provides all of the "launch" capabilities for Docker. We'll be using it to create new containers.

    ```bash
    docker run -i -t ubuntu /bin/bash
    ```

  The `-i` flag keeps `STDIN` open from the container, even if we're not attached to it. The `-t` flag tells Docker to assign a pseudo-tty to the container we're about to create. This provides us with an interactive shell in the new container.
* The container only runs for as long as the command we specified, `/bin/bash`, is running. Once we exited the container, that command ended, and the container was stopped.
* You can use the `docker ps` with the `-a` flag to show all containers, or `-l` flag to show the last container that was run, whether stopped or running.
* There are 3 ways containers can be identified: a short UUID, a longer UUID and a name.
* If we don't specify a name for the container using `--name` flag, Docker will automatically generate a random name. A valid container name can contain the following characters: a to z, A to Z, 0 to 9, underscore, period, and dash. Names are unique.
* To create a daemonized container, we use `docker run` with `-d` flag.
* You can use `docker logs` to see logs of a container. Use `docker logs -f` to monitor logs, `docker logs --tail 10` to get the last ten lines of a log, and `docker logs --tail 0 -f` to follow the logs of a container without having to read the whole log file.
* Since Docker 1.6, you can also control the logging driver used by your daemon and container by passing `--log-driver` option to the daemon or the `docker run` command. Default is `json-file` which provides the behavior we've just seen using the `docker logs` command. Also available is `syslog` which disables `docker logs` command and redirects all container log output to Syslog. Lastly, also available is `none`, which disables all logging in containers and results in the `docker logs` command being disabled. Additional logging drivers continue to be added. Docker 1.8 introduced support for Graylog's GELF protocol, Fluentd and a log rotation driver.
* We can use `docker top` command to inspect the processes running inside the container.
* Docker 1.5.0 introduced `docker stats` command to show statistics for one or more containers. We can see a list of containers and their CPU, memory and network and storage I/O performance and metrics.
* Since Docker 1.3 we can also run additional processes inside containers using `docker exec` command. There're 2 types of commands we can run inside a container: **background** and **interactive**. Since Docker 1.7 we can use the `-u` flag to specify a new process owner for `docker exec` launched process.
* We can configure Docker to restart exited containers using the `--restart` flag. It checks for the container's exit code and makes a decision whether or not to restart it. The default behavior is to not restart containers at tall.

    ```bash
    docker run --restart=always --name daemon-dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
    ```

  If `--restart` is set to `always`, Docker will try to restart the container no matter what exit code is returned. Alternatively we can specify a value of `on-failure` which restarts the container if it exits with a non-zero exit code. The `on-failure` flag also accepts an optional restart count.

    ```bash
    --restart=on-failure:5
    ```

  This will attempt to restart the container a maximum of 5 times if a non-zero exit code is received.
* The `docker inspect` is used to get more information about our containers. It will interrogate the containers and return their configuration information, including names, commands, networking configuration, and a wide variety of other useful data. We can also selectively query the inspect results hash using the `-f` or `--format` flag with Go template.

    ```bash
    docker inspect --format='{{ .State.Running }}' daemon-dave
    # => false
    docker inspect --format='{{ .NetworkSettings.IPAddress }}' daemon-dave
    # => 172.17.0.2
    ```

* You can see all your images, containers and container configuration inside `/var/lib/docker` directory.
* You can delete all containers using the following command

    ```bash
    docker rm `sudo docker ps -a -q`
    ```

  The `sudo docker ps -a -q` will return IDs of all containers and then pass them to `docker rm` command.
