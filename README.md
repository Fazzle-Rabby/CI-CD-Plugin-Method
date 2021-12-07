# DevOps Project CI-CD Pipeline Plugin Method

Developer > Git-Hub > Jenkins > Ansible > Docker-Host

# ci

// Build Triggers
GitHub hook trigger for GITScm polling

// Send files or execute command over ssh:
rsync -avh /var/lib/jenkins/workspace/ci/Dockerfile root@172.31.17.160:/opt

// Send files or execute command over ssh:
cd /opt
docker image build -t $JOB_NAME:v1.$BUILD_ID .
docker image tag $JOB_NAME:v1.$BUILD_ID fazzlerabby/$JOB_NAME:v1.$BUILD_ID
docker image tag $JOB_NAME:v1.$BUILD_ID fazzlerabby/$JOB_NAME:latest
docker image push fazzlerabby/$JOB_NAME:v1.$BUILD_ID
docker image push fazzlerabby/$JOB_NAME:latest
docker image rmi  $JOB_NAME:v1.$BUILD_ID  fazzlerabby/$JOB_NAME:v1.$BUILD_ID  fazzlerabby/$JOB_NAME:latest

# cd

// Build Triggers
ci
Trigger only if build is stable

// Send build artifacts over ssh:
ansible-playbook  /sourcecode/docker.yml

- hosts: all
  tasks:
    - name: stop container
      shell: docker container stop docker-container
    - name: remove container
      shell: docker container rm docker-container
    - name: remove image
      shell: docker image rm fazzlerabby/ci
    - name: create conbtainer
      shell: docker container run -itd --name docker-container -p 9000:80 fazzlerabby/ci
