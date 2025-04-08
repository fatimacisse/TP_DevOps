#commandes docker

docker build -t image_finapp:1 .
docker images
docker-compose down
docker-compose up -d |  docker-compose up -d --build
docker ps -a  
hostname -I
docker ps
docker logs finance_app
docker rm finance_app
docker rm finance_db
docker rmi e46e06f3ccb5
docker-compose up -d
docker exec -it finance_db mysql -u root -p



#commandes SQL
SHOW TABLES;
SHOW DATABASES;
SELECT DATABASE();
USE db_paymybuddy;
INSERT INTO `user` (`email`, `password`, `firstname`, `lastname`, `balance`) VALUES ("security@gmail.com", 'passer', 'Security', 'User', 0.00);
SELECT * FROM `user`;


#commandes git
git remote -v
git remote remove origin
git remote add origin git@github.com:fatimacisse/TP_DevOps.git
git remote -v
git branch
git push -u origin main

# J'ai pu creer les conteneurs et deployer l'application. Cependant je rencontre un probleme avec la base de donnee
# je n'ai pas pu integrer les donnees lors de l'initialisation des conteneurs
# j'ai aussi essaye la methode des env et des secrets mais ca ne marche pas non plus
