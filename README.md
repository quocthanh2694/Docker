# Docker
## Setup
### Docker toolbox
Download Docker toolbox and install (check download Git & Install virtual box NDISS driver - If have error => don't check driver NDISS)
=> link error fix sang docker for desktop: https://stackoverflow.com/questions/36885985/cannot-start-docker-after-installation-on-windows
### Docker for desktop

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

# Run (Powershell on win 10)
# Commands in Docker
- ```docker images``` show all images in docker
- ```docker run -ti --rm hello-world sleep 3``` for test docker (--rm: remove container after stop; sleep 3: after 3 seconds container will auto exit)
- ```docker run -ti ubuntu bash -c "sleep 3; echo job finished" --rm``` sleep 3 seconds and print text.
- ```docker run -ti -d ubuntu bash``` run ubuntu background and go back to docker.

- ```docker attach container_name_or_id``` go inside container by name or id "container_name_or_id`" (container_name get from ```docker ps```).
- ``` docker exec -ti compassionate_mccarthy bash``` go inside container parallel with ```docker attach container_name_or_id``` by name "compassionate_mccarthy". When main process exit => this exec will be exit.

 - ```docker create -ti ubuntu bash``` create container without run. Status of container will be "Created" (view in ```docker ps -a```)
 - ```docker start/stop/restart -ai 8b16398778a0``` start/stop/restart docker by dockerId "8b16398778a0" (dockerId get from ```docker ps -a```)
 - ``` docker cp ebook.txt pensive_lovelace:/root/ebook.txt``` copy file ebook.txt to docker by name "pensive_lovelace" (dockerName get from ```docker ps```)
 -```docker inspect 688030a8b8ba | grep IPAddr``` get information like: network, driver, ip... => return json ("| grep IPAddr" is optional for search "IPAddr")
 -```docker rm containerNameOrId``` remove docker container by name or Id, Note: Make sure container is stopped.
- ```docker ps``` show containers are running.
- ```docker ps -a``` show containers are running and stopped.
- ```docker ps -l``` show container has just stopped.
- ```docker run --network=host -ti ubuntu:16.04 bash``` run ubuntu as bash (like git bash)
- ```docker commit container_id``` to create image from container by container id (container id get from ```docker ps -a```)
- ```docker tag 6440eb149adb ubuntu_new``` rename 'ubuntu_new' for imageId '6440eb149adb' (imageId get from ```docker images```)
- ```docker commit f65fa7938c08 ubuntu_2``` create image from container id with name 'ubuntu_2'.


# Commands in LINUX:
 - ```pwd``` check current path in linux are staging
 - ```cat /etc/lsb-release``` or ```cat /etc/*-release``` get current system information. 
 - ```exit``` exit ubuntu.
 - ```touch file_name``` create new file with name "file_name". 
 - ```Ctrl + C or Ctrl + D``` to exit and stop container.
 - ```Ctrl + P / Ctrl + Q``` to exit container but keep container running.
 
 # Return code 
 (Docker website have list of exit code)
 - 0 exit success
 - 125 exit when run docker have error.
 - 126 exit when script cannot run
 - 130 script exit by 'Ctrl+C / Ctrl+D'


 
 
 
 
