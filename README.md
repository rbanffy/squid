# Squid | Ubuntu

Current Squid Docker Image from Ubuntu. Receives security updates and rolls to newer Squid or Ubuntu LTS. This repository is exempted from per-user rate limits. For [LTS Docker Image](https://ubuntu.com/security/docker-images) versions of this image, see `lts/squid`. 


## About Squid

Squid is a caching proxy for the Web supporting HTTP, HTTPS, FTP, and more. It reduces bandwidth and improves response times by caching and reusing frequently-requested web pages. Squid has extensive access controls and makes a great server accelerator. It runs on most available operating systems, including Windows and is licensed under the GNU GPL.


## Tags and Architectures
![LTS](https://assets.ubuntu.com/v1/0a5ff561-LTS%402x.png?h=17)
Up to 5 years free security maintenance `from lts/squid`.

![ESM](https://assets.ubuntu.com/v1/572f3fbd-ESM%402x.png?h=17)
Up to 10 years customer security maintenance `from store/canonical/squid`.

_Tags in italics are not available in ubuntu/squid but are shown here for completeness._

| Channel Tag | | | Currently | Architectures |
|---|---|---|---|---|
| **`4.13-21.10_beta`** &nbsp;&nbsp; | | | Squid 4.13 on Ubuntu 21.10 | `amd64`, `arm64`, `ppc64el`, `s390x` |
| _`track_risk`_ |

Channel tag shows the most stable channel for that track ordered `stable`, `candidate`, `beta`, `edge`. More risky channels are always implicitly available. So if `beta` is listed, you can also pull `edge`. If `candidate` is listed, you can pull `beta` and `edge`. When `stable` is listed, all four are available. Images are guaranteed to progress through the sequence `edge`, `beta`, `candidate` before `stable`.


## Usage

Launch this image locally:

```sh
docker run -d --name squid-container -e TZ=UTC -p 3128:3128 ubuntu/squid:4.13-21.10_beta
```
Access your Squid proxy at `localhost:3128`.

#### Parameters

| Parameter | Description |
|---|---|
| `-e TZ=UTC` | Timezone. |
| `-p 3128:3128` | Expose the proxy service |
| `-v /path/to/configuration:/etc/squid` | Directory with squid configuration files |
| `-v /path/to/logs:/var/log/squid` | Volume to store squid logs |
| `-v /path/to/data:/var/spool/squid` | Volume to store the squid cache |


#### Testing/Debugging

To debug the container:

```sh
docker logs -f squid-container
```

To get an interactive shell:

```sh
docker exec -it squid-container /bin/bash
```


## Deploy with Kubernetes

Works with any Kubernetes; if you don't have one, we recommend you [install MicroK8s](https://microk8s.io/) and `microk8s.enable dns storage` then `snap alias microk8s.kubectl kubectl`.

Download
[squid.conf](https://git.launchpad.net/~canonical-server/ubuntu-docker-images/+git/squid/plain/examples/config/squid.conf) and
[squid-deployment.yml](https://git.launchpad.net/~canonical-server/ubuntu-docker-images/+git/squid/plain/examples/squid-deployment.yml) and set `containers.squid.image` in `squid-deployment.yml` to your chosen channel tag (e.g. `ubuntu/squid:4.13-21.10_beta`), then:

```sh
kubectl create configmap squid-config --from-file=squid=squid.conf
kubectl apply -f squid-deployment.yml
```

You can now access the squid proxy on port 3128

## Bugs and feature requests

If you find a bug in our image or want to request a specific feature, please file a bug here:

[https://bugs.launchpad.net/ubuntu-docker-images/+filebug](https://bugs.launchpad.net/ubuntu-docker-images/+filebug)

Please title the bug "`squid: <issue summary>`". Make sure to include the digest of the image you are using, from:

```sh
docker images --no-trunc --quiet ubuntu/squid:<tag>
```


