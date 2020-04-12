### How to move docker storage from home directory to other location 
======================
    Caution - These steps depend on your current /var/lib/docker being an actual directory (not a symlink to another location).

    1) Stop docker: service docker stop. Verify no docker process is running: ps aux | grep -i [d]ocker

    2) Double check docker really isn't running. Take a look at the current docker directory: ls /var/lib/docker/

    2b) Make a backup - tar -zcC /var/lib docker >
      /mnt/pd0/var_lib_docker-backup-$(date +%s).tar.gz

    3) Move the /var/lib/docker directory to your new partition: mv /var/lib/docker /mnt/pd0/docker

    4) Make a symlink: ln -s /mnt/pd0/docker /var/lib/docker

    5) Take a peek at the directory structure to make sure it looks like it did before the mv: ls /var/lib/docker/ (note the trailing slash)

    6) Start docker back up service docker start

    7) restart your containers (resolve the symlink)
    
  ===================================
