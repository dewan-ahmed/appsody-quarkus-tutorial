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
Log-out and log back in for the above changes to reflect on your account.

### Installing Appsody:

Get the latest version from [Appsody Installation Doc](https://appsody.dev/docs/getting-started/installation/) and update the following code/version, if required.
```
wget https://github.com/appsody/appsody/releases/download/0.4.9/appsody_0.4.9_amd64.deb
sudo apt install -f $PWD/appsody_0.4.9_amd64.deb
```
Once the above steps are done, type in **appsody** and hit enter. If you see something like the following, your installation was successful:
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
The above step would pull the latest docker image for your stack and end with the confirmation:
**Successfully initialized Appsody project**

### Build and run your first cloud-native application

```
appsody build
appsody run
```
If you closely follow the results of **appsody build**, you'll see some familiar docker build outputs:
```
.
.
.
Docker]  ---> e40b4c0eeacb
[Docker] Step 2/34 : COPY . /project
[Docker]  ---> ef9dcfcd6ec9
[Docker] Step 3/34 : WORKDIR /project/user-app
[Docker]  ---> Running in 9d9d4c82b29c
[Docker] Removing intermediate container 9d9d4c82b29c
[Docker]  ---> e1017234a9d3
[Docker] Step 4/34 : COPY ./user-app/src ./src
[Docker]  ---> f46c2d44e4f3
[Docker] Step 5/34 : COPY ./user-app/pom.xml ./
[Docker]  ---> 1893cd5f123d
[Docker] Step 6/34 : USER root
[Docker]  ---> Running in 606a1dfda109
[Docker] Removing intermediate container 606a1dfda109
[Docker]  ---> 94658d3e6ee5
[Docker] Step 7/34 : RUN chown -R quarkus .
[Docker]  ---> Running in d3868b8820cd
[Docker] Removing intermediate container d3868b8820cd
[Docker]  ---> 21d4005b3998
[Docker] Step 8/34 : USER quarkus
[Docker]  ---> Running in dfacb5b40cdf
[Docker] Removing intermediate container dfacb5b40cdf
[Docker]  ---> 1b46a4645c9c
[Docker] Step 9/34 : RUN mvn -B -Pnative clean package
[Docker]  ---> Running in 1a3d50d73670
.
.
.
```
Then appsody downloads the required maven dependencies from maven central for your quarkus build (using docker under the hood):
```
.
.
.
[Docker] [INFO] Downloading from central: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-compiler-plugin/3.1/maven-compiler-plugin-3.1.jar
[Docker] [INFO] Downloaded from central: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-compiler-plugin/3.1/maven-compiler-plugin-3.1.jar (43 kB at 1.2 MB/s)
[Docker] [INFO] Downloading from central: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.22.1/maven-surefire-plugin-2.22.1.pom
[Docker] [INFO] Downloaded from central: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.22.1/maven-surefire-plugin-2.22.1.pom (5.0 kB at 208 kB/s)
[Docker] [INFO] Downloading from central: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.22.1/maven-surefire-plugin-2.22.1.jar
.
.
.
```
**appsody run** would have your containerized application running; by default on port 8080 for quarkus. If you go to localhost:8080 or yourServerIpAddress:8080, you should see the following message:
> Congratulations, you have created a new Quarkus application.

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
