# Advanced-Docker
### File IO
* `FileIO/Dockerfile` is the docker file for the first container that writes to a sample text file
  * Build a new image for this docker container : `docker build -t echo .`
  * Run this container : `docker run -d --name echo echo`
* `FileIO/second_container/Dockerfile` is the docker file for the second container that links to the 1st container
  * Build an image for this container : `docker build -t ping .`
  * Link this container to the 1st container as : `docker run -t -i --link echo:FileIO ping curl FileIO:9001`
* Screencast for `File IO` : https://raw.githubusercontent.com/okeashwin/Advanced-Docker/master/File%20IO/HW4_FileIO.mp4

### Ambassador pattern
* Configured two VMs on Vagrant for this task.
* On `VM1`, Redis server and a Redis ambassador is setup while on `VM2`, Redis client and a Redis Ambassador is setup
  * Instructions for setting up `VM1`
    * `vagrant init dbit/ubuntu-docker-fig`
    * To enable communication between the two VMs, we uncomment `config.vm.network "private_network", ip: "192.168.33.10"` in the `Vagrantfile`
    * `vagrant up`
    * We need to start the docker-compose service on VM1 : `vagrant ssh; sudo docker-compose up -d`
  * Instructions for `VM2`
    * `vagrant init dbit/ubuntu-docker-fig`
    * `vagrant up ; vagrant ssh`
    * Run `redis_client` on this VM by : `sudo docker-compose run redis_client`
    * We can now test this functionality using `redis-cli` on VM2 : `set key "devops" ; get key` ( `get key` should return `devops`
* Screencast for `Ambassador Pattern` : https://raw.githubusercontent.com/okeashwin/Advanced-Docker/master/Ambassador%20Pattern/HW4_AmbassadorPattern.mp4

### Docker Deploy
* Execute `init.sh` for setting up the registry and building `blue-slice` and `green-slice` images for the first time
* Setup bare `git` repos ( as done in the Deployment workshop)
* A `post-commit` hook is set up in the App that builds a new docker image and pushes it to the registry.
* `git push blue master` pushes the changes to the blue slice, which can be verified by `curl localhost:50100`
* Green changes can be verified by `curl localhost:50101`
* Screencast for `Docker-Deploy` : https://youtu.be/-oZH_crwdzU
