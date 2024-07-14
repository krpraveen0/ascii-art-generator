#### ASSCI ART GENERATOR
### Steps to deploy this applicaiton
Step 1: Building the application
To build the application above run the following command in the terminal. The command./mvnw clean package utilizes Maven to clean the project by removing previous build artifacts and subsequently packages the Java project, compiling the source code and creating a distributable package, often in the form of a JAR file.

```./mvnw clean package```

On a successful build, you will get a log like below and under the target directory, you can see the jar file for the application.


Build success log
Step 2: Add the Dockerfile

```
FROM eclipse-temurin:21-jdk-alpine
VOLUME /tmp
COPY target/ascii-art-generator-0.0.1-SNAPSHOT.jar ascii-art-generator.jar
ENTRYPOINT ["java","-jar","/ascii-art-generator.jar"]
```
This Dockerfile is designed to package the ASCII art generator into a Docker container. It utilizes the Eclipse Temurin (AdoptOpenJDK) Alpine base image with Java 21, offering a lightweight and efficient container environment. The JAR file of the application located at target/ascii-art-generator-0.0.1-SNAPSHOT.jar , is copied into the root directory of the container and renamed as ascii-art-generator.jar. Finally, the default entry point is set to execute the Java application using the specified JAR file, ensuring the seamless deployment and execution of the ASCII art generator within the Dockerized environment. This Dockerfile streamlines the packaging process, making the deployment of the Java application consistent and reproducible across various environments.

Step 3: Build the Docker Image
Once the Dockerfile has been added to the root directory, you can run the command below to generate the Docker image. Make sure that you have docker installed on your system. If not you can follow the doc here

This generated docker image will then be stored in your local system.

```docker build -t ascii-art-generator .```

Step 4: Logging into Dockerhub
To push the Docker image to Dockerhub, you need to log in using the following command:

```docker login```
Make sure to provide appropriate credentials when prompted.

Step 5: Tagging the Docker Image
Now, tag the image with the following command:

```docker tag ascii-art-generator <username>/ascii-art-generator:latest```

This will create a new repository <username>/ascii-art-generator and will push the image ascii-art-generator when executing the next step.
Note: above username is your dockerhub username.

Step 6: Pushing the Docker Image to Dockerhub
Now it’s time to push the tagged Docker image to Dockerhub using the command:

```docker push ascii-art-generator```
The image will be successfully pushed to your Dockerhub repository.

Alternatively, if you have Docker Desktop installed you can directly deploy the image to the Docker hub from here


Docker hub push in Docker Desktop
Step 7: Deploying the application on Render
Log on to render.com, you will land on the dashboard page which will look something like the below, Click on New and select the Web Service option.

Render dashboard
Select Deploy an existing image from a registry and click Next.

Now you can head over to DockerHub and copy the pull command from the tags tab for the image you want to deploy.

With that let's head over back to render and paste it in the next step and click Next.

Now you can give a name to your Web Service, select a region and instance type( Select the free one) and click on Create Web Service. Your Spring Boot application is now successfully deployed on render.com


Note that the free instance will spin down in case of Inactivity for some time. It can take up to 50 seconds for it to spin up again causing performance delays.