# mzac/docker-snmpd
Docker image to provide snmpd in situations where it's difficult (like CoreOS & Home Assistant)

[![GitHub issues](https://img.shields.io/github/issues/mzac/docker-snmpd.svg?style=flat-square)](https://github.com/mzac/docker-snmpd/issues) [![GitHub license](https://img.shields.io/github/license/mzac/docker-snmpd.svg?style=flat-square)](https://github.com/mzac/docker-snmpd/blob/master/LICENSE)
[![Docker Pulls](https://img.shields.io/docker/pulls/mzac23/docker-snmpd.svg?style=flat-square)](https://hub.docker.com/r/mzac23/docker-snmpd/)

Quick and Dirty
---------------

Launch listening on "public" like this:
```
docker run -d \
  -v /proc:/host_proc \
  --privileged \
  --read-only \
  -p 161:161/udp \
  --name snmpd \
  mzac23/docker-snmpd
```

On Home Assistant OS
--------------------

- Enable privileged mode for the SSH container
- SSH to your Home Assistant Host

```
docker run -d \
  -v /proc:/host_proc \
  --privileged \
  --read-only \
  --net host \
  --name snmpd \
  mzac23/docker-snmpd
```

Your own snmpd.conf
-------------------

```
docker run -d -v /my/snmpd.conf:/etc/snmp/snmpd.conf \
  -v /proc:/host_proc \
  --privileged \
  --read-only \
  -p 161:161/udp \
  --name snmpd \
  mzac23/docker-snmpd
```

Important Notes
---------------

- Containers don't have access to /proc - so you must provide it per the examples above.
- snmpd has been modified to use /host_proc for your convenience.
