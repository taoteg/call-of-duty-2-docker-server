# GitHub & Node.js app

This Dockerfile is built on top of Ubuntu and allow launching a Node.js app in a container.

## Usage :
You will need to :

1. Have your node app **repository on github**;
2. **Generate** an SSH key pairs and add the public key to your github account [as explained in the GitHub help](https://help.github.com/articles/generating-ssh-keys/) (you can also use an existing one if you have done this step previously);
3. Copy your generated SSH private key next to this Dockerfile;
4. **Edit the Dockerfile** to paste over your GitHub repositry URI on the **<YOUR\_GITHUB\_REPOSITORY\_HERE>**. It should follow this format : **https://github.com/YOUR\_USER\_NAME/YOUR\_NODE\_APP\_REPOSITORY\_NAME.git**.
5. You can now **build** your docker image & **run** your docker container hosting your app (useful for CD-like workflow).

`docker build -t nodeapp .`
> Don't forget the dot (**.**) at the end or it won't read your dockerfile.

`docker run -d nodeapp`
> You can drop the "-d" flag if you want the direct console output, altougth exiting the console will kill your container.
