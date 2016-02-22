---
date: 2015-05-02
title: How to access docker containers from external devices
is: Post
categories:
  - Docker
  - HTTP Proxy
---
The solution proposed on this post doesn't apply only to docker containers but to any service you run in a local private network. By local private network I mean any kind of network that you can only access locally, from your computer, examples of these networks are NAT based VMs, docker network or a private VPN.

Docker gives you the power to run the same application image on both development and production environments.

To be able to route traffic to a specific container it is common to run a reverse-proxy on ports 80/443. Given the hostname the reverse-proxy redirect traffic to the specific docker container. There is famous docker image named [nginx-proxy](https://registry.hub.docker.com/u/jwilder/nginx-proxy/) that waits for docker events (container start/stop), modifies nginx configuration and reloads it, enabling you to define virtual hosts on demand. Check its docker image page for more information.

The strategy mentioned above works for both production and development environment. On production environment the nginx-proxy docker container will be exposed on ports 80 and 443, mapped to respective ports 80 and 443 of the host machine. In addition to that you must define DNS entries pointing to the host machine.

To simulate the production environment on development environment you have two alternatives:

1. Map a hostname to the docker interface (or to a VM interface in case of running docker inside a VM), e.g. `local.bravi.com.br` that points to `10.10.10.10` (our default VM ip address at Bravi);
1. Modify the `/etc/hosts` file in host and possibly in vm machines to add hostname entries pointing to the private ip address;

Both solutions work very well. I definitely recommend the first one, you can map an Internet DNS wildcard host pointing to your docker/vm ip address and by doing that you don't need to manually add a new entry for each new docker container you want to run. At [Bravi](http://www.bravi.com.br) we take the first option and we have to domain name `*.local.bravi.com.br` pointing to `10.10.10.10` (the fixed ip address we assign to our Virtual Machine running Docker on it).

You might be asking now:

> "Ok, everything is running as I expected, I can access from my computer any of my docker containers, when I hit http://my-service.local.bravi.com.br it resolves to `10.10.10.10` that is my VM IP address, on my VM I have `nginx-proxy` running and mapped to ports 80/443 and I also have my service container running with the `VIRTUAL_HOST` environment variable with value `my-service.local.bravi.com.br` set, so `nginx` will reverse-proxy traffic on virtual host `my-service.local.bravi.com.br` to my service container, but **how can I access it from an external device? I want to test my service from a physical mobile device or from another VM running IE.**"

# The solution

The easiest solution I've found for the problem mentioned above is to run an HTTP(S) proxy on your host machine, by doing this, everything that connects to it will have access to all networks available on your host machine, the naming resolution will also be done by your host machine. In case you setup you mobile phone to use your host's machine proxy, you will be able to open mobile browser and hit an internal ip address / host, e.g. `10.10.10.10`, `localhost`, etc.

I've decided to build my own HTTP(S) proxy, a very simple one that is focused on this specific problem and it is focused on development environment. I'm not good at names so I named it [my-proxy](https://github.com/esnunes/my-proxy). Here is a diagram showing how it works:

<img src="https://raw.githubusercontent.com/esnunes/my-proxy/master/docs/usage-example.png" style="width: 100%;" />

You can find more information about it, its architecture and how it works [here](https://github.com/esnunes/my-proxy).
