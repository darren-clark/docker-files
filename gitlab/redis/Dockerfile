from sameersbn/redis

#fixup postgres user to match our worker uuid
run groupmod -g 1000 redis
run usermod -u 1000 -g 1000 redis
