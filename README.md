# Using docker requires sudo
* Create the docker group.

```shell
sudo groupadd docker
```
* Add your user to the docker group.

```shell
sudo usermod -aG docker $USER
```
* still non user have permission issue.
```shell
docker ps -a

Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.26/containers/json?all=1: dial unix /var/run/docker.sock: connect: permission denied
```
* Looking at the permissions of the socket indicated in the error message, /var/run/docker.sock:

```shell
ls -l /var/run/docker.sock
```
```
srw-rw---- 1 root root 0 Apr 18 12:46 /var/run/docker.sock
```
* Changing the permissions on this socket is enough to allow non-sudo use:
```shell
sudo chmod 666 /var/run/docker.sock
ls -l /var/run/docker.sock
```
```
srw-rw-rw- 1 root root 0 Apr 18 12:46 /var/run/docker.sock
```
```
docker run hello-world
```
```
Hello from Docker!
```
This message shows that your installation appears to be working correctly.
