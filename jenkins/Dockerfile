from jenkins

user root

run apt-get update && apt-get install -y netcat && rm -rf /var/lib/apt/lists/*

run groupadd -g 999 docker
run usermod -a -G docker jenkins

user jenkins

