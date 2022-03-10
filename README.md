# docker-tomcat-tutorial
A basic tutorial on running a web app on Tomcat using Podman (based on a docker tutorial)

# Steps
* Install [podman] (https://podman.io/getting-started/installation).
* Clone this repository - $git clone https://github.com/emverdes/docker-tomcat-tutorial.git
* cd 'docker-tomcat-tutorial'
* $podman build -t tomcat-demo:1 .
* $podman run -p 8008:8080 --name demo1 tomcat-demo:1
* http://localhost:8008
* Run another instance for load balancing $podman run -p 8009:8080 --name demo1 tomcat-demo:1

# Apache proxy loadbalancer
<Proxy "balancer://mycluster">
    BalancerMember "http://localhost:8008/sample"
    BalancerMember "http://localhost:8009/sample"
</Proxy>
ProxyPass        "/" "balancer://mycluster/"
ProxyPassReverse "/" "balancer://mycluster/"


# For reverse proxy
* #setsebool -P httpd_can_network_connect on
* #setsebool -P httpd_can_network_relay on


# Links
[Sample Tomcat web app](https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/)
