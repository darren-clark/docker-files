# docker-files

Contains Docker build files for various uses.

So far has what I used to build a scm/ci environment using Jenkins and Gitlab. 

The primary change was to ensure that all the containers use the same UID/GID for the main process. That simplifies creation
of storage only containers, as well as maintenance of users on the host system. 
