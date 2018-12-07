1) **Installing docker**: 

We will use nvidia-docker, intatlation instructions is [here](https://github.com/NVIDIA/nvidia-docker#ubuntu-140416041804-debian-jessiestretch)

2) **Download builded container**:

```sudo docker pull uber/horovod:0.15.2-tf1.12.0-torch0.4.1-py3.5```

if you have an error "unauthorized: authentication required" here, try to generate a key at https://ngc.nvidia.com/configuration/api-key and type ```docker login nvcr.io```.

3) **Run container in background**: 

```sudo nvidia-docker run --detach -it uber/horovod:0.15.2-tf1.12.0-torch0.4.1-py3.5```

4) **List of containers**:

```sudo nvidia-docker ps```

It will looks like that:

```
ars@ars:~$ sudo nvidia-docker ps
CONTAINER ID        IMAGE                                           COMMAND             CREATED             STATUS              PORTS               NAMES
b36bdc52e0a1        uber/horovod:0.15.2-tf1.12.0-torch0.4.1-py3.5   "/bin/bash"         7 minutes ago       Up 7 minutes                            stupefied_merkle
```

5) **Enter insede the container (attach)**:

```
sudo docker attach b36bdc52e0a1
```

6) **Exit container witout stoping it (detach)**: 

```
Ctrl + p + q
```

7) **Save container state (installed packages)**:

To save it you need to "commit" changes by the following command:

```
sudo docker commit b36bdc52e0a1 arsashuha/horovod:v1
```

check that everything is fine

```
ars@ars:~$ sudo docker images
REPOSITORY          TAG                                IMAGE ID            CREATED             SIZE
arsashuha/horovod   v1                                 c217b65a597d        8 seconds ago       6.21GB
uber/horovod        0.15.2-tf1.12.0-torch0.4.1-py3.5   c73fe5ca1f47        5 days ago          5.91GB
```

8) **Comit ypur container to repos**:

Create login at ```https://hub.docker.com``` and use [this](https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html) instruction. 

```nvidia-docker push arsashuha/horovod:v2```

_Be careful do not make your code available online!_

9) **Data transfer**:

You can have a shared folder between your pc and container by adding ```-v <pc_folder>:<conntainer_folder>``` to run command.

```sudo nvidia-docker run --detach -it -v ~/Downloads:/home uber/horovod:0.15.2-tf1.12.0-torch0.4.1-py3.5```
