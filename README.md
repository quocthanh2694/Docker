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
- ```docker run -ti hello-world``` for test docker
- ```docker ps``` show containers are running.
- ```docker ps -a``` show containers are running and stopped.
- ```docker ps -l``` show container has just stopped.
- ```docker run --network=host -ti ubuntu:16.04 bash``` run ubuntu as bash (like git bash)
- ```Ctrl + C or Ctrl + D``` to exit.
- ```docker commit container_id``` to create image from container by container id (container id get from ```docker ps -a```)
- ```docker tag 6440eb149adb ubuntu_new``` rename 'ubuntu_new' for imageId '6440eb149adb' (imageId get from ```docker images```)
- ```docker commit f65fa7938c08 ubuntu_2``` create image from container id with name 'ubuntu_2'.


# Commands in LINUX:
 - ```pwd``` check current path in linux are staging
 - ```cat /etc/lsb-release``` get current system information. 
 - ```exit``` exit ubuntu.
 - ```touch file_name``` create new file with name "file_name". 
 
 # Return code 
 (Docker website have list of exit code)
 - 0 exit success
 - 125 exit when run docker have error.
 - 126 exit when script cannot run
 - 130 script exit by 'Ctrl+C / Ctrl+D'


 
 
 
 
