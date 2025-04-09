#image de base utilisee
FROM amazoncorretto:17-alpine

#responsable de maintenir le dockerfile
LABEL maintainer="Mame Fatima CISSE"

# Copy de l artefact dans mon conteneur
COPY target/paymybuddy.jar /app/paymybuddy.jar

#Identifie le repo /app comme le repertoir courant de travail
WORKDIR /app


EXPOSE 8080

#Commande par defaut qui sera utilisee pour executer l application
CMD ["java", "-jar", "paymybuddy.jar"]


