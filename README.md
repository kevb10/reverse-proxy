# Background
I have one Digital Ocean droplet with an IP address of 123.23.123.45. I want it to serve multiple websites/apps.

# Goals
- [x] Show my portfolio at kevinmanase.com
- [x] Run my blog at blog.foussa.io
- [x] Have a front for foussa.io
- [x] All of those accessible from both wwww.domain.com & domain.com 
- [ ] Also accessible from `http` & `https`
- [ ] Do all of that with Traefik

# What's working
I can access blog.foussa.io, monitor.foussa.io, db-admin.foussa.io

# What's not working
- ~~I get a bad getaway or 404 when I access foussa.io, kevinmanase.com~~
- `https` doesn't seem to work when I use a `docker-compose` for the proxy
It works when I use the following command
```
docker run -d \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $PWD/traefik.toml:/traefik.toml \
  -v $PWD/acme.json:/acme.json \
  -p 80:80 \
  -p 443:443 \
  -l traefik.frontend.rule=Host:monitor.foussa.io \
  -l traefik.port=8080 \
  --network web \
  --name traefik \
  traefik
  ```
but the certificate is bad
