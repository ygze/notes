spark Tutorial

### Setting(CentOS)

#### Install Java
  * Download JAVA 8 on CentOS:
  ```
  cd /opt/
wget –no-cookies –no-check-certificate –header “Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie” “http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.tar.gz”
tar xzf jdk-8u151-linux-x64.tar.gz
  ```

 * Insall JAVA
 ```
 cd /opt/jdk1.8.0_151/
alternatives –install /usr/bin/java java /opt/jdk1.8.0_151/bin/java 2
alternatives –config java

 ```
 * It is recommended to setup javac and jar commands path using alternatives
 ```
 alternatives –install /usr/bin/jar jar /opt/jdk1.8.0_151/bin/jar 2
 alternatives –install /usr/bin/javac javac /opt/jdk1.8.0_151/bin/javac 2
 alternatives –set jar /opt/jdk1.8.0_151/bin/jar
 alternatives –set javac /opt/jdk1.8.0_151/bin/javac
 ```
 * Setup Java Environment
 ```
 vi ~/.bash_profile
 export JAVA_HOME=/opt/jdk1.8.0_151
 export JRE_HOME=/opt/jdk1.8.0_151/jre
 export PATH=$PATH:/opt/jdk1.8.0_151/bin:/opt/jdk1.8.0_151/jre/bin
 ```

 #### Install Hadoop
