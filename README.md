# linux-ubuntu-jenkins-ci
Quick jenkins setup guide for building CI pipeline


Technical stack 

* Ubuntu server
* Java 17 or 21 as per July 2025

#### Step1:  system update
```
sudo apt-get update -y
```
![update](./assets/20250717170435.png)

#### Step2: Install Java17
```
sudo apt-get install openjdk-17-jdk -y
```
![install](./assets/20250717170605.png)


#### Step3: Install Jenkins from Official 

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

```
sudo apt-get install jenkins -y
```

![install](./assets/20250717171259.png)

#### Step4: For some reason if it fails. Check the error using this.

```
sudo -u jenkins /usr/bin/jenkins
```
#### Step5: Check Jenkins is running or not and start if not.

```
sudo systemctl status jenkins
sudo systemctl daemon-reload

sudo systemctl restart jenkins
sudo systemctl status jenkins
```

#### Step6: Check it is running without error.

```
sudo systemctl status jenkins
```

![status](./assets/20250717171853.png)

#### Step 7: Access the Jenkins to work with it.

```
http://server-ip-address:8080
```
![access](./assets/20250717175218.png)

#### Step 8:
Incase remove the current setup.

```
sudo systemctl stop jenkins
sudo apt remove jenkins -y 
sudo rm -rf /var/lib/jenkins/
```
#### (optional) 
If u installed older version of java like to switch to this Java 17 version follow this.

```
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-17-openjdk-amd64/bin/java 1

sudo update-alternatives --config java

java -version
```

#### (optional) 
Make sure Jenkins points to the latest installed Java. 
```
sudo systemctl edit jenkins

[Service] 
Environment="JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64"
```

and default points to the latest installed Java.

![latest](./assets/20250717170904.png)

That's all. Start building with Jenkins!:-)
