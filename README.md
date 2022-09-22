# Install-MySQL-server-on-Docker-EC2

Before installing the MySQL update the server 

```
sudo apt-get update
````

```
sudo apt-get upgrade
````

```
sudo apt update
````

```
sudo apt upgrade
````

***install docker****

```
curl -fsSL https://get.docker.com -o get-docker.sh
````
```
sh get-docker.sh
````
```
exit
````

***Login Again***

```
sudo usermod -aG docker $USER 
````

To check the Docker Containers
```
docker ps -a
````
If you get permission denied execute the below command

```
sudo chmod 666 /var/run/docker.sock
````

Create directory and save my.cnf file

```
mkdir /my/custom
````
```
sudo nano my.cnf
````

past the below lines in the file and save

```
[mysqld]
# Accept connections from any IP address
bind-address                =0.0.0.0
````

Run docker image 

```
sudo docker run --name mysql8.0.13 -p 3306:3306 -v /my/custom:/etc/mysql/ -e MYSQL_ROOT_PASSWORD=root -d mysql/mysql-server:8.0.13
````

Once docker image created, go into to the docker image

```
docker exec -it $containerID bash
````

bind the IP address 0.0.0.0

```
mysqld --verbose --help | grep bind-address
````

this should display the below cmds

```
[mysqld]
# Accept connections from any IP address
bind-address                =0.0.0.0
```

Login to the mysql user and give the authentications

```
mysql -u root -p
````

execute the below lines tow give authentication to user and IP address to connect from outside workbench 
```
mysql> CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
````
```
mysql> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost' WITH GRANT OPTION;
````
```
mysql> CREATE USER 'monty'@'%' IDENTIFIED BY 'some_pass';
````
```
mysql> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'%' WITH GRANT OPTION;
````
```
mysql> FLUSH PRIVILEGES;
````
and now exit.

