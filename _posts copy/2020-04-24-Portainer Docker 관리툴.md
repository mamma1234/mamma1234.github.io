---
layout: post
title: 'Portainer Docker 관리툴'
description:
headline:
modified: 2020-04-24
category: webdevelopment
imagefeature:
tags: [Portainer Docker 관리툴]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Portainer

sudo usermod -aG docker $USER

sudo docker volume create portainer_data

docker run -d --restart=always --name portainer -p 9001:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /home/volumes/portainer_data:/data portainer/portainer
