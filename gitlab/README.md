# GitLab

This install is based on the excellent images from [Sameer Naik](https://hub.docker.com/u/sameersbn/).

The full deployment separates the three processes for [GitLab] (http://gitlab.com) into their own containers. This include a container for Redis, a container for Postgres, 
and a container for GitLab itself.

There are Dockerfiles here for Redis and Postgres that change the UID of the respective process user to 1000. This makes it easier(at least for me) to manage the storage 
only containers host users. I have a UID 1000 on the host system simply named ``docker-worker``, so I don't have UID overlaps and can properly see access controls.

To build and bring up a full GitLab:

```Shell
docker build --tag gitlab-redis redis
docker build --tag gitlab-postgres postgres
docker run --name gitlab-redis-storage -v /var/lib/redis ubuntu useradd -U -d /var/lib/redis redis
docker run --name gitlab-redis --volumes-from gitlab-redis-storage gitlab-redis
docker run --name gitlab-postgres-storage -v /var/lib/postgresql ubuntu useradd -U -d /var/lib/postgresql postgres
docker run --name gitlab-postgres --volumnes-from gitlab-postgres -e DB_NAME=gitlabhq_production -e DB_USER=gitlab -e DB_PASS=pass gitlab-postgres
docker run --name gitlab-storage -v /home/git/data ubuntu useradd -U -d /home/git/data git
docker run --name gitlab --volumes-from gitlab-storage -e GITLAB_PORT=8081 -e GITLAB_SSH_PORT=8022 -p 8081:80 -p 8022:22 --link gitlab-postgres:postgresql --link gitlab-redis:redisio sameersbn/gitlab
```  

And now a self contained GitLab server on port 8081 of your host.
