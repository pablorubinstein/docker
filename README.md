You need to have `docker-compose` installed in your system (see https://docs.docker.com/compose/install/) 

 1. edit contents of pxe.env
 1. make sure you have internet access and run 
 ```
env $(cat pxe.env | xargs) docker-compose build
 ```
 This will build the 3 required images
 1. now change your network settings and set a static IP suing the same IP addres specified in pxe.env
 1. start the compose 
 ```
docker-compose up 
 ```
 You should now be able to PXE boot and install an ESXi on any vm that is in the same network (hint: set networking mode of PXE servre and target machine to 'internal')



