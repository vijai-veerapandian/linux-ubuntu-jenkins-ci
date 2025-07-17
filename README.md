# linux-ubuntu-jenkins-ci
quick jenkins setup guide for building CI pipeline


Technical stack 

* Ubuntu server
* Java 17 or 21 as per July 2025

### Step1:  system update
```
sudo apt-get update -y
```
![[Pasted image 20250717170435.png]](./assets/Pasted image 20250717170435.png).

### Step2: Install Java17
```
sudo apt-get install openjdk-17-jdk -y
```
![[Pasted image 20250717170605.png]]


### Step3: (optional) If u installed older version of java like to switch to this Java 17 version follow this.
```
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-17-openjdk-amd64/bin/java 1

sudo update-alternatives --config java

java -version
```

![[Pasted image 20250717170904.png]]

#### Step5: Install Jenkins from Official 

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

```
sudo apt-get install jenkins -y
```

![[Pasted image 20250717171259.png]]

#### Step5: For some reason if it fails. Check the error using this.

```
sudo -u jenkins /usr/bin/jenkins
```


#### Step6: (optional) Make sure Jenkins points to the latest installed Java. 
```
sudo systemctl edit jenkins

[Service] 
Environment="JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64"
```

and default points to the latest installed Java.

![[Pasted image 20250717171003.png]]

#### Step7: Check Jenkins is running or not and start if not.

```
sudo systemctl status jenkins
sudo systemctl daemon-reload

sudo systemctl restart jenkins
sudo systemctl status jenkins
```


#### Step8: Check it is running without error.

```
sudo systemctl status jenkins
```

![[Pasted image 20250717171853.png]]

#### Step 9: Access the Jenkins to work with it.

```
http://server-ip-address:8080
```

#### Step10: (Final and Optional). Incase remove the current setup.

```
sudo systemctl stop jenkins
sudo apt remove jenkins -y 
sudo rm -rf /var/lib/jenkins/
```


That's all.Happy playing with Jenkins!
