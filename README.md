# Docker
## Setup
### Docker toolbox
Download Docker toolbox and install (check download Git & Install virtual box NDISS driver - If have error => don't check driver NDISS)

=> link error fix sang docker for desktop: https://stackoverflow.com/questions/36885985/cannot-start-docker-after-installation-on-windows
### Docker for desktop
- Check versions:
- docker -v
- docker-compose -v
- docker-machine -v
1. Install Docker Community Edition (not Docker Toolbox)
2. Enable Hyper-V
Open Control Panel -> System and Security -> Programs (left panel) -> Turn Windows features on or off -> Check the Hyper-V box

As of 2017's Win 10, if you don't have Hyper-V option, then your Windows OS is not Enterprise Edition. Also, Docker seems to work a lot better on Intel processors (not AMD).

3. Add C:\Program Files\Docker\Docker\resources\bin to Path in Environmental Variables.
4. Open Git Bash and type docker-compose up and now that command should work.
If you don't have GitBash, please download it.

## Note
- Image is snapshot and can create many container independency
- Container Independence: Docker container do not save anything in image. It's only save inside container while it's running
- Avoid container get dependence when start. Make sure get dependence from inside container => avoid host dependence die.
- Don't let impotant files in container stoped and have no name. Done work for a long time on a container have no name and not back up data because you will remove container is stopped for save hard disk or clean trash. => Usually let Name for container and back up files.
- Docker hub search registry: https://hub.docker.com/ 

## Connect container together
### Way 1: connect via host
1. In a powershell 1 run ```docker run -ti --rm -p 112:113 ubuntu:14.04 bash``` "-p 112:113": port input outside container - 112, port input inside container - 113.
2. ```nc -l 113``` netcat listen port 113
3. Run another powershell 2 run another unbutu: ```docker run -ti --rm ubuntu:14.04 bash```
4. ```nc  172.29.125.209 112```: '172.29.125.209' is ip get from ipconfig
5. input text from powershell 1 => auto print in powershell 2
### Way 2: connect directly from container 1 to 2, just one way
1. In powershell 1 (pw1) run ```docker run -ti --rm --name server ubuntu:14.04 bash```
2. In pw1 run ```nc -l 111``` 
3. In pw2 run ```docker run --rm -ti --link server --name client ubuntu:14.04 bash``` (--link server: connect to container have name = 'server')
4. In pw2 run ``` nc server 111``` listen to server port 111.
5. Input data from pw1 or pw2 => auto output the other pw1 or pw2.


# Run (Powershell on win 10)
# Commands in Docker
- ```docker images``` show all images in docker
- ```docker run -ti --rm hello-world sleep 3``` for test docker (--rm: remove container after stop; sleep 3: after 3 seconds container will auto exit)
- ```docker run -ti ubuntu bash -c "sleep 3; echo job finished" --rm``` Run command inside bash: sleep 3 seconds and print text.
- ```docker run --name app -ti -d ubuntu bash``` run ubuntu background and go back to docker (d: detach). Name for container "app"

- ```docker attach container_name_or_id``` go inside container by name or id "container_name_or_id`" (container_name get from ```docker ps```).
- ```docker logs app``` show log of container. "app" is the name of container.
- ``` docker exec -ti compassionate_mccarthy bash``` go inside container parallel with ```docker attach container_name_or_id``` by name "compassionate_mccarthy". When main process exit => this exec will be exit.

 - ```docker create -ti ubuntu bash``` create container without run. Status of container will be "Created" (view in ```docker ps -a```)
 - ```docker start/stop/restart -ai 8b16398778a0``` start/stop/restart docker by dockerId "8b16398778a0" (dockerId get from ```docker ps -a```)
 - ``` docker cp ebook.txt pensive_lovelace:/root/ebook.txt``` copy file ebook.txt to docker by name "pensive_lovelace" (dockerName get from ```docker ps```)
- ```docker inspect 688030a8b8ba | grep IPAddr``` get information like: network, driver, ip... => return json ("| grep IPAddr" is optional for search "IPAddr"). 
- ```docker rm containerNameOrId``` remove docker container by name or Id, Note: Make sure container is stopped.
- ```docker kill containerNameOrId``` stop docker container by name or Id.
- ```docker ps``` show containers are running.
- ```docker ps -a``` show containers are running and stopped.
- ```docker ps -l``` show container has just stopped.
- ```docker run --network=host -ti ubuntu:16.04 bash``` run ubuntu as bash (like git bash)
- ```docker commit container_id``` to create image from container by container id (container id get from ```docker ps -a```)
- ```docker tag 6440eb149adb ubuntu_new``` rename 'ubuntu_new' for imageId '6440eb149adb' (imageId get from ```docker images```)
- ```docker commit f65fa7938c08 ubuntu_2:v1.0``` create image from container id with name 'ubuntu_2' and tag version "v1.0" (version default will be "latest"). Name structure: registry.repo.com:port/organization/image-name:version-tag (registry.repo.com:port is OPTIONAL)
- ```docker run --memory="198m"``` limit memory 256mb

- ```docker pull debian:latest``` pull newest debian
- ```docker tag debian:latest quocthanh2694/image-1:v1.0``` create name for image prepare for push
- ```docker push  quocthanh2694/image-1:v1.0``` push on docker hub quocthanh2694

IMAGES:
- ```docker rmi image_name:version image_name -f``` remove multiple images by name:version (-f: force)
- ```docker save -o backup-images.tar.gz debian:latest custom-centos``` back multiple images (debian:latest,  custom-centos) with name:version. "o" mean output.
- ```docker load -i backup-images.tar.gz``` load backup images.

VOLUMN: 

Share data container and host (you can exit container without lose files shared)
- ```docker run -ti -v C:\Users\admin/host_data:/container_data ubuntu bash``` : "-v" mean volumn. "C:\Users\admin/host_data" folder host; "/container_data" folder share data inside unbutu.

Share data between container. (exit all container will be lose any files in shared folder)
- ``` docker run -ti --name pc1 -v /share ubuntu bash``` run pc1 with folder share inside ubuntu.
- ```echo data > /share/data_file``` create new file with data.
- ``` docker run -ti --name pc2 --volumes-from pc1 ubuntu bash``` run pc2 with volumes from pc1 => with folder "/share" from pc1.
- => pc1 and pc2 are use the same sharing folder name: share.
- Stop pc1 and start pc3 also volumes to pc2 => get the same file and folder in share folder.
- If stop pc3 and pc2 (stop all pc have share folder) => share folder will be destroy.


DOCKER FILE

Ex1: Build hello world Dockerfile
- create folder example, cd to example folder and create file "Dockerfile" (Capital "D") with content
```FROM busybox
RUN echo "This is the most basic Dockerfile."
CMD echo "Welcome on board."
```
- ```docker build -t basic . ``` build image name "basic" from Dockerfile. ( -t: tag, ". end of command mean current folder have Dockerfile")
- ``` docker run --rm basic ``` => You will see text "Welcome on board.".

Ex2: install and run command exc Dockerfile
- Content of Dockerfile: 
```FROM debian:sid
RUN apt-get -y update
RUN apt-get install nano
CMD ["/bin/nano","/text/dummy"]
```

NGINX:
- ```docker run -d -p 8081:80 --name webservere3 nginx``` run nginx port 8081 (on browser need to get ip from ipconfig like: http://192.168.56.1:8081/)
- ```docker run --name ng -d -P nginx``` run nginx on random port
# Commands in LINUX:
 - ```pwd``` check current path in linux are staging
 - ```cat /etc/lsb-release``` or ```cat /etc/*-release``` get current system information. 
 - ```exit``` exit ubuntu.
 - ```touch file_name``` create new file with name "file_name". 
 - ```Ctrl + C or Ctrl + D``` to exit and stop container.
 - ```Ctrl + P / Ctrl + Q``` to exit container but keep container running.
 - ```cat /etc/hosts``` 
 - ```df -h``` print information about disk and storage.
 - ```echo data > /share/data_file``` create file with name "data_file" in folder share and have content: data.
 
 # Return code 
 (Docker website have list of exit code)
 - 0 exit success
 - 125 exit when run docker have error.
 - 126 exit when script cannot run
 - 130 script exit by 'Ctrl+C / Ctrl+D'


 
 
 
 
