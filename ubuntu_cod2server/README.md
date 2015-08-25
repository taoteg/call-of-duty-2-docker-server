# Call of Duty 2 server

This dockerfile create an image to deploy a [Call of Duty 2](https://en.wikipedia.org/wiki/Call_of_Duty_2) multiplayer server on Ubuntu.

## Prerequisite

You need the following things :

1. the linux dedicated server binary, which can be found in this repository ;
2. the orginal game, as it's content is used by the dedicated server ;
3. [docker](https://www.docker.com/) installed and configured on your host machine, obviously.

## Usage (unix)

Clone or download the repository and follow theses steps to get ready :

1. un-tar the dedicated server in the `cod2server` folder : `cd cod2server && tar xvfj cod2-lnxded-1.3-06232006.tar.bz2`
2. copy the required data from the game to the server :
  1. go in the `main` folder of your original game ;
  2. copy all the `iw_XX.iwd` from 00 to **14** to the `cod2server/main` folder (you want to keep the 15 already in place, as it was unpacked from the dedicated server) ;
  3. copy all the localization `localized_english_iwXX.iwd` to the `cod2server/main` (it might be another language).
3. go back to the root folder where you downloaded the repository, and build the docker image : `docker build -t cod2server .` (don't forget the **dot** at the end). It might take some times as the main folder is pretty heavy (~3.7 GB).
4. launch the container : `docker run -d -p 28960:28960/udp cod2server`.

## Notes

* The host machine used was an ubuntu server 14.04.3 LTS
* You might want to use a separated user to launch your docker container. In this case do not forget to add him to the docker group : `sudo gpasswd -a USER\_NAME docker`, and restart docker dameon : `sudo service docker restart`.
* You also might want to [automate the container startup at server boot](https://docs.docker.com/articles/host_integration/).
* There is a similar repository on github which propose a Call of Duty 2 server based on CentOS : [hberntsen/docker-cod2](https://github.com/hberntsen/docker-cod2)
* The gcc3-libs in the `cod2server` folder was used as a workaround before finding a proper solution to add it using official repositories (32 / 64 bit runtime issues). It is not used anymoer but will stay here as a backup, just in case it would not be supported anymore.

## TODO
- add config.cfg
