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

## Run (Powershell on win 10)
### Download ubuntu 16.04
 - ``` docker run --network=host -ti ubuntu:16.04 bash```
 - ```Ctrl + C or Ctrl + D``` to exit.
