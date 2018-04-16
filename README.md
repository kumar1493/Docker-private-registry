# Docker-private-registry


I have attached two file. One is playbook & other is daemon.json file.

save the daemon.json file in /etc/docker if you are running ubuntu/redhat. For windows it has different path & same path we need to give in playbook under "src" Highlighted below.
You need to replace the IP in the daemon.json file with the IP of the server which is being used for registry.

- name: Making registry open to public
  copy: 
      src: /etc/docker/daemon.json
      dest: /etc/docker/daemon.json
      mode: 0644
      owner: root
      group: root

Run the playbook and it will ensure the public access of the registry.
You need to use the below commands to push or pull from registry:-

Run these commands from external server other than registry which has docker installed in it.
Restart docker service at both ends after playbook run.

$ docker pull ubuntu:16.04
$ docker tag ubuntu:16.04 <IP>:5000/my-ubuntu
$ docker push <IP>:5000 /my-ubuntu
$ docker pull <IP>:5000 /my-ubuntu

I checked at my end and it is working perfectly fine.
I have used an insecure way for that : https://docs.docker.com/registry/insecure/

I have also attached the logs for playbook & push/pull commands execution.
