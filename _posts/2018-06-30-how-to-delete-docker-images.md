---
title:  How to delete docker images
tags:
  - Linux
  - docker
---

Here's how to delete docker images.

<!--more-->

1.Run those commands in a shell:

Warning: This will destroy all your images and containers. It will not be possible to restore them!
```bash
#!/bin/bash
# Delete all containers
docker rm $(docker ps -a -q)
# Delete all images
docker rmi $(docker images -q)
```
