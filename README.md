# Step to configure
I will used this app to learn performace testing using K6.
## 1. Setup Database
In this project, i'm using container to running the databases. 
```bash
# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Enable user to runnig docker command without using sudo
groupadd docker
sudo usermod -aG docker $USER
sudo chmod 666 /var/run/docker.sock

# Running mysql container and the configuration
docker network create -d k6
docker run -d --name mysql --network k6 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=database mysql:latest
docker exec -it mysql sh

# Running in the shell command of container
mysql -u root -p -h localhost -P 3306   # --> type root as a password
CREATE DATABASE belajar_k6;
USE belajar_k6;
SHOW TABLES;
```
## 2. Setup application
```bash
# Clone the project repository
mkdir belajar-k6
cd belajar-k6
git clone https://github.com/ProgrammerZamanNow/belajar-nodejs-restful-api.git .
npm install

# Setting the db url to DATABASE_URL="mysql://root:root@<your_ip>:3306/belajar_k6"
# Setting prisma config at migrations/../migration.sql then delete "ENGINE InnoDB"

npx prisam migrate dev
npx prisma generate
```
