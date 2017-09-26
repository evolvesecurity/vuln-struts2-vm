# A Vulnerable Apache Struts Application

**Confirmed Vulnerabilities**

| CVE       | Description                                   | URL                                                          |
|-----------|-----------------------------------------------|--------------------------------------------------------------|
| 2017-5638 | Remote Command Vulnerability in Apache Struts | https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5638 |

**Requirements:**

* [Vagrant](https://www.vagrantup.com/docs/installation/)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [SearchSploit](https://www.virtualbox.org/wiki/Downloads) (Optional)

**Setup**

```
$ git clone https://github.com/evolvesecurity/vuln-struts2-vm.git
$ cd vuln-struts2-vm
```

**Build Virtual Machine**

**IMPORTANT:** The VM currently uses "public networking" (See: Vagrantfile). This should only be used on a secure LAN. Otherwise, "private networking" should be used.

See: https://www.vagrantup.com/docs/virtualbox/networking.html

```
$ vagrant up # this will raise and provision your machine
$ vagrant ssh
# to get the IP of your machine if unknown:
ubuntu@strut $ ip route
```

**Verification:**

You should no visit http://IP:8080 to see if tomcat8 is working. If the url is unavailable, try http://IP:8080/manager with the credentials "tomcat" and "tomcat".

**Exploitation:**

Open one terminal and create a socket

```
# download exploit from https://www.exploit-db.com/exploits/41570/
# or use searchsploit
$ searchsploit Struts #optional
$ cp /path/to/linux/webapps/41570.py exploit.py
$ python exploit.py "http://IP:8080/http-session/hello.action" "cmd"
```

It may be necessary to modify your exploit.py in order to pass in the command you want.

One option to confirm your exploit is to simply setup a netcat listener and connect back to it.

**Troubleshooting:**

If you wish to ssh directly into your vm without using the ```vagrant ssh``` command, you need to set a password for the ubuntu user. First, ssh into the vm using ```vagrant ssh``` and then perform a password reset using ```passwd ubuntu```.

**Credits:**

The source code for the Apache Struts2 applications was taken from https://github.com/apache/struts-examples. The pom.xml files were modified slightly in order to downgrade Apache Struts2 to a vulnerable version.
