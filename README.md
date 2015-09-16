# Call of Duty 2 server

This dockerfile create an image to deploy a [Call of Duty 2](https://en.wikipedia.org/wiki/Call_of_Duty_2) multiplayer server on Ubuntu .

## Prerequisite

You need the following things :

1. the linux dedicated server binary, which can be found in this repository ;
2. the orginal game, as it's content is used by the dedicated server ;
3. A host machine of your choice with x86_64 architecture
4. [docker](https://www.docker.com/) installed and configured on your host machine, obviously.

## Usage (unix)

Clone or download the repository and follow theses steps to get the server up and running :

1. copy the required data from the game to the server :
  1. go in the `main` folder of your original game (install directory or retail DVD);
  2. copy all the `iw_XX.iwd` from 00 to **14** to the `cod2server/main` folder (you want to keep the 15 already in place, as it was unpacked from the dedicated server) ;
  3. copy all the localizations `localized_english_iwXX.iwd` to the `cod2server/main` (it might be another language).
2. go in the `docker` folder, and build the docker image : `docker build -t cod2server .` (don't forget the **dot** at the end).
3. launch the container : `docker run -it -d -p 28960:28960/udp -p 20510:20510/udp -v /path/to/cod2server:/home/cod2/cod2server cod2server`. Don't forget to update the path of the `cod2server` folder in the docker command to fit your configuration. 
4. Depending on your setup, you might have some port-forwarding to do.

> We use [docker volumes](https://docs.docker.com/userguide/dockervolumes/) to read the game files & configuration : our local `cod2server` folder is mounted in our container. It allow us to update the configuration without rebuilding the docker image : we only have to relaunch the container after changes.

## Notes

* There is a similar repository on github proposing a Call of Duty 2 server based on CentOS : [hberntsen/docker-cod2](https://github.com/hberntsen/docker-cod2)
* The host machine used for this setup was an ubuntu server 14.04.3 LTS x86_64 architecture.
* You might want to use a separated user to launch your docker container. In this case do not forget to add him to the docker group : `sudo gpasswd -a USER\_NAME docker`, and restart docker dameon : `sudo service docker restart`.
* You also might want to [automate the container startup at server boot](https://docs.docker.com/articles/host_integration/) with the `--restart=always` flag.
* The config file located in `cod2server/main/config.cfg` can be edited to suits your needs.
* You will find original and modified `cod2_lnxded` dedicated server binaries in the `backup` folder. It might be usefull if you want to create a cracked server to play on without a CD key. But you won't need this as you did buy the game, didn't you ? 

> if you didn't, [this](http://killtube.org/showthread.php?1337-CoD2-Tutorial-How-to-make-your-cracked-server-show-up-in-the-master-list) might help your pervert mind create a masterlist-visible-pirate-uberawesome server.

* The gcc3-libs in the `cod2server` folder was used as a workaround before finding a proper solution to add it using official repositories (32 / 64 bit gcc library issues as dicussed [here](http://askubuntu.com/questions/454253/how-to-run-32-bit-app-in-ubuntu-64-bit/454254#454254)). It is not used anymore but will stay here as a backup, just in case it would not be supported anymore.

## Docker

If you are not familiar with docker (docker engine, docker hub, dockerfiles, docker images and containers), I suggest you have a look at the [documentation](https://docs.docker.com/) (especially the [dockerfiles](https://docs.docker.com/reference/builder/) part).

I also strongly recommend reading the [best practices for writing dockerfiles](https://docs.docker.com/articles/dockerfile_best-practices/) for a better understanding and a cleaner writing of dockerfiles.

**[Docker](https://www.docker.com/) is awesome**, give it a try ;-)
