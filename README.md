# appsody-quarkus-tutorial
A quick tutorial on how to build a cloud-native application using Appsody and Quarkus 

## Taking care of the pre-requisites

These steps are executed on linux(Ubuntu 18.04) but you can follow similar steps for Windows/Mac. If stuck, please reach out to author via [GitHub](https://github.com/dewan-ahmed).

### Installing Java

Get the latest version from [openJDK](https://jdk.java.net)
During the time of this tutorial, version 13.0.1 is the latest. Update the following code to the jdk version you're using.

```
wget https://download.java.net/java/GA/jdk13.0.1/cec27d702aa74d5a8630c65ae61e4305/9/GPL/openjdk-13.0.1_linux-x64_bin.tar.gz
tar xvf openjdk-13.0.1_linux-x64_bin.tar.gz
export JAVA_HOME=$PWD/jdk-13.0.1/
export PATH=${PATH}:${JAVA_HOME}/bin
```

### Installing Docker

```
sudo curl -sSL https://get.docker.com/ | sh
sudo usermod -aG docker dewan
sudo systemctl start docker
sudo systemctl enable docker
```

### Installing Appsody:

Get the latest version from [Appsody Installation Doc](https://appsody.dev/docs/getting-started/installation/) and update the following code/version, if required.
```
wget https://github.com/appsody/appsody/releases/download/0.4.9/appsody_0.4.9_amd64.deb
sudo apt install -f $PWD/appsody_0.4.9_amd64.deb
```
Once the above steps are done, type in *appsody* and hit enter. If you see something like the following, your installation was successful:
```
The Appsody command-line tool (CLI) enables the rapid development of cloud native applications.

Complete documentation is available at https://appsody.dev

...
...
...
```

### Creating your first Appsody project using Quarkus stack

Quarkus is an experimental stack and things might be in flux. Please submit PR to [Appsody GitHub](https://github.com/appsody) if you find an issue.  
```
mkdir my-project
cd my-project
appsody init experimental/quarkus
```

### Run your first cloud-native application

```
appsody run
```

Out-of-the-box, Appsody gives you the following endpoints for various metrics on your running application

- Health Endpoint: http://localhost:8080/health
- Liveness Endpoint: http://localhost:8080/live
- Readiness Endpoint: http://localhost:8080/ready
- Metrics Endpoint: http://localhost:8080/metrics
- Performance Dashboard: http://localhost:8080/appmetrics-dash




### Troubleshooting

Experiencing issues with *root* account? Try running as non-root user (with root access) instead.

```
adduser <username>
usermod -aG sudo <username>
su <username>
```
