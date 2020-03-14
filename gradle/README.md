# How to install Gradle in Ubuntu 18.04
**Step 1: Update the System**
```
aathit@workstation:~$ sudo apt-get update
aathit@workstation:~$ sudo apt-get -y upgrade
```
**Step 2:** [Install JDK](https://aathith.github.io/blog/java/)

**Step 3: Download Gradle**
```
aathit@workstation:~$ wget https://services.gradle.org/distributions/gradle-5.2.1-bin.zip
```
**Step 4: Install Gradle**

    aathit@workstation:~$ sudo mkdir /opt/gradle
    aathit@workstation:~$ sudo unzip -d /opt/gradle gradle-5.2.1-bin.zip
    
**Step 5: Set GRADLE_HOME & PATH**

    aathit@workstation:~$ sudo nano /etc/profile.d/gradle.sh
    > export GRADLE_HOME=/opt/gradle/gradle-5.2.1
    > export PATH=${GRADLE_HOME}/bin:${PATH}
    aathit@workstation:~$ source /etc/profile.d/gradle.sh

**Step 6: Check Gradle Version**

    aathit@workstation:~$ gradle -v
    
    ------------------------------------------------------------
    Gradle 5.2.1
    ------------------------------------------------------------
    
    Build time:   2019-02-08 19:00:10 UTC
    Revision:     f02764e074c32ee8851a4e1877dd1fea8ffb7183
    
    Kotlin DSL:   1.1.3
    Kotlin:       1.3.20
    Groovy:       2.5.4
    Ant:          Apache Ant(TM) version 1.9.13 compiled on July 10 2018
    JVM:          1.8.0_242 (Private Build 25.242-b08)
    OS:           Linux 4.15.0-66-generic amd64

### Reference link:
https://www.vultr.com/docs/how-to-install-gradle-on-ubuntu-16-10

(This page is created by AATHITH(myself) for my self-reference only.)

