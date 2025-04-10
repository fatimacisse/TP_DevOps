# Commandes docker

- docker build -t image_finapp:1 .
- docker images
- docker-compose down | docker-compose down -v
- docker-compose up -d ou docker-compose up -d --build
- docker ps -a  
- hostname -I
- docker ps
- docker logs finance_app
- docker rm finance_app
- docker rm finance_db
- docker rmi e46e06f3ccb5
- docker-compose up -d
- docker exec -it finance_db mysql -u root -p
- docker exec -it finance_db ls /docker-entrypoint-initdb.d/
- docker-compose config
  



# Commandes SQL
- SHOW TABLES;
- SHOW DATABASES;
- SELECT DATABASE();
- USE db_paymybuddy;
- SELECT * FROM `user`;


# Commandes git
- git remote -v
- git remote remove origin
- git remote add origin git@github.com:fatimacisse/TP_DevOps.git
- git remote -v
- git branch
- git push -u origin main

# Commentaires et captures

- J'ai pu creer les conteneurs et deployer l'application.
- Apres avoir effectue des tests toutes les fonctionnalites fonctionnent apres deploiement
![page d accueil](https://github.com/user-attachments/assets/3a980d33-43eb-4175-adbd-1718ced07670)

![page d'accueil PMB](https://github.com/user-attachments/assets/39a705a6-ce5c-492b-bdb8-dd5e04e2c2f1)

![Add buddy](https://github.com/user-attachments/assets/b92d3ee6-e1b9-4bca-8475-b6cc84ca6864)

![Deconnexion](https://github.com/user-attachments/assets/2319d4d1-53a9-4103-8205-b0be105e4b17)



- Utilisation de la methode des environnements pour securiser les donnees sensibles. Le fichier .env est visible pour comprendre le fonctionnement. Cependant il est preferable de placer le fichier .env dans .gitignore.


# Commandes pour la creation du registry prive + push de mon image 'image_finapp'

#creation d'un conteneur registry-app pour le backend de mon registry prive
- docker run -d -p 5000:5000 --net  mini-projet-docker_default --name registry-app registry:2.8.1

#creation d'un conteneur frontend-registry pour le frontend de mon registry prive
- docker run -d -p 9090:80 --net mini-projet-docker_default -e NGINX_PROXY_PASS_URL=http://registry-app:5000 -e DELETE_IMAGES=true -e REGISTRY_TITLE=Myregistry --name frontend-registry joxit/docker-registry-ui:2

- docker ps -a
  
#tag de mon image afin de pouvoir le push vers mon registry prive
- docker tag image_finapp:1 192.168.56.7:5000/image_finapp:1

- docker images

#premier essaie pour push mon image
- docker push 192.168.56.7:5000/image_finapp:1 
#voici le message d'erreur:
#erreur https This error occurs because Docker is trying to communicate with your private registry over HTTPS, but the registry is configured to use HTTP. Here's how you can resolve this issue


#si dessous la configuration de docker afin d'acceder au registre prive via HTTP au lieu de HTTPS
- sudo vi /etc/docker/daemon.json
	{
  "insecure-registries": ["192.168.56.7:5000"]
        }

#on redemarre docker et on allume les conteneurs
-  sudo systemctl restart docker
- docker start registry-app  
- docker start frontend-registry  

#deuxieme essaie de push l'image et c'est un success
- docker push 192.168.56.7:5000/image_finapp:1

- Url pour acceder au registry prive : http://192.168.56.7:9090/

# Captures du registry
#Accueil

![registry prive](https://github.com/user-attachments/assets/8d0b296c-9ee7-4084-9e0f-f96e84cf7264)

#Image
![registry prive2](https://github.com/user-attachments/assets/e28eb45d-46a9-4c7b-9ad7-429ed39bfaa4)




