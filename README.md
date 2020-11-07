# Rancher step by step

**First step:** \
Make sure you have Docker installed.

**Second step:** \
We need to run the Rancher Server with some commands, ex.:
  
```
sudo docker run -d \
  --restart=unless-stopped \
  --name rancher \
  -p 80:80 \
  -p 443:443 \
  -v /opt/rancher:/var/lib/rancher \
  --privileged \
  rancher/rancher:v2.5.1 --no-cacerts
```
The `--no-cacerts` will make sure https://rancher_url/v3/settings/cacerts is empty. \
**Remember**, this is optional. \
This solve the problem: `x509: certificate signed by unknown authority` 

The `--privileged` solve kubernetes privileged requirements on the latest versions of rancher.

To use with DNS, and auto-gernerate certificate, just need to add a parameter, like this:

```
sudo docker run -d \
  --restart=unless-stopped \
  --name rancher \
  -p 80:80 \
  -p 443:443 \
  -v /opt/rancher:/var/lib/rancher \
  --privileged \
  rancher/rancher:v2.5.1 \
  --acme-domain mydoamin.com
```

**Third step:** \
  We need to use rancher-cli official image for run the commands(You can make for yourself an image).
```  
  1. rancher login HOST TOKEN
  2. rancher ps # for see the k8s deployments
  3. rancher kubectl set image deployments/nginx nginx=nginx:latest # for update a deployment
```  
 
Whith this we can use Rancher CLI commands, for example in Continuous Integration. \
\
Enjoy it :D
