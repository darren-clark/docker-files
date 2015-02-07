from sameersbn/postgresql

#fixup postgres user to match our worker uuid
run groupmod -g 1000 postgres
run usermod -u 1000 -g 1000 postgres
run chown -R postgres.postgres /etc/postgresql/*
