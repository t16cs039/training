# How to use cpp

## docker command

- to use cpp and share test folder.

```shell
$ docker build . -t cpp
$ docker load -i docker-repo/cpp

$ docker image ls

$ docker run -d -v "/Users/nakadats/training/cpp/test:/nakadats/cpp/test" --name cpp -i -t cpp

$ docker ps -a

$ docker container exec -it cpp bash
```

- after using cpp.

```shell
$ exit
```

```shell
$ docker ps -a

$ docker stop cpp

$ docker rm cpp

$ docker ps -a

$ docker image ls

$ docker image rm cpp

$ docker image ls
```