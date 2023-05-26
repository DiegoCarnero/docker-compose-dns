# docker-compose-dns
Example of a custom DNS implementation with bind9 for a Docker Compose project, additionally allowing communication between hosts in different networks using their hostnames.

To test this project you can simply use:
```
docker compose up
```

As is, this system allows name resolution only. If you want to establish any type of connection across networks you need to define new rules on your firewall settings.
To do so on linux see: https://stackoverflow.com/a/51373066
```
sudo iptables -I DOCKER-USER -i br-########1 -o br-########2 -j ACCEPT
sudo iptables -I DOCKER-USER -i br-########2 -o br-########1 -j ACCEPT
```
To remove these rules:
```
sudo iptables -L --line-numbers  # see rule indices
sudo iptables -D DOCKER-USER 1  # delete rule with num 1
```