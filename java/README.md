# Install JAVA
This page will show you **How to install JAVA in UBUNTU 18.04**
## Run these Commands:
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
java -version
```
## Change default java version:
```
sudo update-alternatives --config java
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```
Enter the number from `Selection` column and press `Enter`.

### Reference links:
[https://linuxize.com/post/install-java-on-ubuntu-18-04/](https://linuxize.com/post/install-java-on-ubuntu-18-04/)<br>
[https://www.geofis.org/en/install/install-on-linux/install-openjdk-8-on-ubuntu-trusty/](https://www.geofis.org/en/install/install-on-linux/install-openjdk-8-on-ubuntu-trusty/)

(This page is created by AATHITH(myself) for my self-reference only.)

