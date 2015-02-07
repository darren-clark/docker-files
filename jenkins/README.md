# Jenkins

Modified library/jenkins to allow builds to control Docker on the host system.

Modifications:
 1. Add the ``docker`` group
 2. Add ``jenkins`` user to ``docker`` group

Note that the GID currently hardcoded(to what it ended up on my Ubuntu 14.04 host).

This should be able to be made scriptable on startup and passable via environment.

For my setup I use the library/ubuntu container as a storage only container, and built this image tagged ``jenkins-docker``

To bring up the container use:

```Shell
docker run --name jenkins-storage -v /var/jenkins_home useradd -U -d /var/jenkins_home jenkins-docker
docker run -d --name jenkins --volumes_from jenkins-storage -v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 jenkins-docker
```

Now you have a Jenkins CI server available on port 8080 of the host!
