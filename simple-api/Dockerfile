# --- Build stage ---
FROM eclipse-temurin:21-jdk-alpine AS myapp-build
ENV MYAPP_HOME=/opt/myapp
WORKDIR $MYAPP_HOME

# maven pour builder
RUN apk add --no-cache maven

# cache maven: copier d'abord pom.xml, pré-télécharger les deps
COPY pom.xml .
RUN mvn -q -DskipTests dependency:go-offline

# puis copier le code et builder
COPY src ./src
RUN mvn -q package -DskipTests

# --- Run stage ---
FROM eclipse-temurin:21-jre-alpine
ENV MYAPP_HOME=/opt/myapp
WORKDIR $MYAPP_HOME
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","myapp.jar"]