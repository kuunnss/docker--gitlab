## 记录一次docker gitlab搭建踩坑


```
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/etc/gitlab \
  --volume /srv/gitlab/logs:/var/log/gitlab \
  --volume /srv/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
```

22端口向外映射的时候没有改端口，导致gitlab的和sshd的冲突了
git pull&push的时候无法验证

需要改下gitlab.rb中的配置，将port号从22改成4022
然后重启服务
