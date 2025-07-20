[![Github Action (master)](https://github.com/cyber-dojo-languages/ubuntu-build-essential-24.04/actions/workflows/main.yml/badge.svg)](https://github.com/cyber-dojo-languages/ubuntu-build-essential-24.04/actions)

## image_name="ghcr.io/cyber-dojo-languages/ubuntu-build-essential-24.04"

The docker image will not build in Ubuntu 24.04 because the Dockerfile.base is augmented with
extra commands (to fulfil runner's requirements). For example: 
```Dockerfile
RUN (getent group sandbox) || (addgroup --gid 51966 sandbox)
```
There is no addgroup command in the ubuntu:24.04 image and initial attempts to install the shadow-utils
package have failed.

Also:
```Dockerfile
RUN (grep -q sandbox:x:41966 /etc/passwd) || (adduser --disabled-password --gecos "" --home /home/sandbox --ingroup sandbox --shell /bin/bash --uid 41966 sandbox)
```
There is no adduser command in the ubuntu:24.04 image.
This can be fixed with:
```Dockerfile
RUN apt-get update
RUN apt-get install --yes adduser
RUN (grep -q sandbox:x:41966 /etc/passwd) || (adduser --disabled-password --gecos "" --home /home/sandbox --ingroup sandbox --shell /bin/bash --uid 41966 sandbox)
```

![cyber-dojo.org home page](https://github.com/cyber-dojo/cyber-dojo/blob/master/shared/home_page_snapshot.png)
