[![Github Action (master)](https://github.com/cyber-dojo-languages/ubuntu-build-essential-24.04/actions/workflows/main.yml/badge.svg)](https://github.com/cyber-dojo-languages/ubuntu-build-essential-24.04/actions)

## image_name="ghcr.io/cyber-dojo-languages/ubuntu-build-essential-24.04"

The docker image will not build in Ubuntu 24.04 because the Dockerfile.base is augmented with
extra commands (to fulfil runner's requirements). For example: 
```Dockerfile
RUN (getent group sandbox) || (addgroup --gid 51966 sandbox)
```
There appears to be no addgroup command in Ubuntu 24.04 and initial attempts to install the shadow-utils
package have failed.

![cyber-dojo.org home page](https://github.com/cyber-dojo/cyber-dojo/blob/master/shared/home_page_snapshot.png)
