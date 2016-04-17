# Port Forwarding in Mac OS Yosemite+

#### 1. Create Forwarding Rule

```bash
sudo vim /etc/pf.anchors/eclipse.tomcat.forwarding
```

content:

```
rdr pass on lo0 inet proto tcp from any to 127.0.0.1 port 80 -> 127.0.0.1 port 8080
rdr pass on lo0 inet proto tcp from any to 127.0.0.1 port 443 -> 127.0.0.1 port 8443
```


#### 2. Reference the rule in Port Forwarding config

```bash
sudo vim /etc/pf-tomcat.conf
```

content:

```
rdr-anchor "forwarding"
load anchor "forwarding" from "/etc/pf.anchors/eclipse.tomcat.forwarding"

```

**Note: put empty newline in the bottom of the file, or it won't work**

#### 3. Apply the Rule

```bash
sudo pfctl -ef /etc/pf-tomcat.conf
```

#### 4. Stop the port forwarding rules

```bash
sudo pfctl -d
```
