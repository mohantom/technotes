Jenkins
==========
Virtualbox, vagrantup.com (spin up Ubuntu in minutes)
Digitalocean.com: create droplets (eg, Ubuntu)

```shell script
mkdir -p /var/Jenkins_home
chown -R 1000:1000 /var/Jenkins_home/
docker run -p 8080:8080 -d --name jenkins jenkins/jenkins:lts
```

Jenkins: configure from UI

- localhost:8080
    - Create new jobs: nodejs example app
    - Manage Jenkins -> Global Tool Configuration

https://github.com/wardviaene/jenkins-docker/blob/master/Dockerfile
bundled with a docker client to access host docker api (sock)

- Jenkins Job DSL
- Install plugin: job DSl 
- Check the job-dsl-plugin online docs

- Jenkins pipelines
- Write the Jenkins build steps in code


Course: Getting Started With Jenkins Continuous Integration
1. Diagram manual process
2. Follow manual steps
3. Get most basic automation working
4. Add each step
5. Never leave the build in a failed state
