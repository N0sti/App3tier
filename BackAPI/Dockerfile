# Étape 1 : Phase de build
FROM maven:3.8.6-amazoncorretto-17 AS myapp-build
# Définir une variable d'environnement pour le répertoire de travail
ENV MYAPP_HOME /opt/myapp
WORKDIR $MYAPP_HOME

# Copier les fichiers nécessaires pour Maven
COPY pom.xml . 
COPY src ./src

# Lancer la compilation avec Maven
RUN mvn package -DskipTests

# Étape 2 : Phase d'exécution
FROM amazoncorretto:17
# Redéfinir le répertoire de travail
ENV MYAPP_HOME /opt/myapp
WORKDIR $MYAPP_HOME

# Copier uniquement le fichier jar compilé depuis l'étape précédente
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar

# Définir le point d'entrée pour lancer l'application
ENTRYPOINT ["java", "-jar", "myapp.jar"]
