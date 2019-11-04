# appsody-quarkus-tutorial
A quick tutorial on how to build a cloud-native application using Appsody and Quarkus 

## Taking care of the pre-requisites

These steps are executed on linux(Ubuntu 18.04) but you can follow similar steps for Windows/Mac. If stuck, please reach out to author [Dewan Ahmed](dewan.ishtiaque@hotmail.com).

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
cd
wget https://github.com/appsody/appsody/releases/download/0.4.9/appsody_0.4.9_amd64.deb
sudo apt install -f $PWD/appsody_0.4.9_amd64.deb
```
