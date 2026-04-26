Docker pgm


sowjanyamurgesh@MS-Laptop ~ % mkdir dev                                                
sowjanyamurgesh@MS-Laptop ~ % cd dev                                                   
sowjanyamurgesh@MS-Laptop dev % touch app.py                  
sowjanyamurgesh@MS-Laptop dev % nano app.py  
print(“hello”)     
            
sowjanyamurgesh@MS-Laptop dev % touch Dockerfile              
sowjanyamurgesh@MS-Laptop dev % nano Dockerfile 
FROM python:3.10
WORKDIR /app
COPY . .
CMD ["python","app.py”]

sowjanyamurgesh@MS-Laptop dev % touch Jenkinsfile                  
sowjanyamurgesh@MS-Laptop dev % docker build -t dev .   
sowjanyamurgesh@MS-Laptop dev % docker images        
sowjanyamurgesh@MS-Laptop dev % docker run dev       
hello
sowjanyamurgesh@MS-Laptop dev % docker tag dev sowjanya2510/dev:v1
sowjanyamurgesh@MS-Laptop dev % docker push sowjanya2510/dev:v1   
sowjanyamurgesh@MS-Laptop dev % docker pull sowjanya2510/dev:v1

sowjanyamurgesh@MS-Laptop dev % pwd 
/Users/sowjanyamurgesh/dev
sowjanyamurgesh@MS-Laptop dev % ls  
app.py		Dockerfile	Jenkinsfile





pipeline {
    agent any

    environment {
        IMAGE = "sowjanya2510/myapp:v1"
        CREDS = "dockerhub-creds"
        // Ensure Jenkins can find Docker CLI
        PATH = "/usr/local/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                // Checkout your main branch
                git branch: 'main', url: 'https://github.com/sowjanya-m025/b.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build Docker image
                sh 'docker build -t myapp .'
            }
        }

        stage('Tag') {
            steps {
                // Tag the image for Docker Hub
                 sh "docker tag myapp ${IMAGE}"
            }
        }

        stage('Login') {
            steps {
                // Login to Docker Hub using Jenkins credentials
                withCredentials([usernamePassword(
                    credentialsId: CREDS,
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }
        
        stage('Push') {
            steps {
                // Push the image to Docker Hub
                sh "docker push ${IMAGE}"
            }
        }
    }
} 







sowjanyamurgesh@MS-Laptop dev % git init
sowjanyamurgesh@MS-Laptop dev % git add .          
sowjanyamurgesh@MS-Laptop dev % git commit -m "initial commit”
sowjanyamurgesh@MS-Laptop dev % git remote add origin https://github.com/sjmhub25/dev.git
sowjanyamurgesh@MS-Laptop dev % git branch -m main               
sowjanyamurgesh@MS-Laptop dev % git push -u origin main

brew services start jenkins-lts

open jenkins login — 
Username - Admin
Password - 9388883f5c0b48da929959d63ba77e7a

Add Docker Hub Credentials in Jenkins

Open Jenkins
Manage Jenkins → Credentials → Configure Credentials
Add:
Kind: Username &amp; Password

Username: sowjanya2510
Password: 
ID: dockerhub-creds


add docker pipeline plugin

Create Jenkins Pipeline Job

Jenkins Dashboard → New Item - dev-pipeline
Select Pipeline
Configure:
Pipeline → Pipeline script from SCM
SCM → Git
Repo URL → https://github.com/sjmhub25/dev.git
Script Path → Jenkinsfile

Step 9: Build Now (manual)






this is the main issue 
note this down whenever there is token issue u should login to docker client client in ur terminal

To use the access token from your Docker CLI client:
1. Run
$ 
docker login -u sowjanya2510
Copy
2. At the password prompt, enter the personal access token.
#2 [internal] load metadata for docker.io/library/python:3.10
#2 ERROR: failed to authorize: failed to fetch oauth token: unexpected status from GET request to https://auth.docker.io/token?scope=repository%3Alibrary%2Fpython%3Apull&service=registry.docker.io: 401 Unauthorized: incorrect username or password
———
like this
docker login -u sowjanya2510

i Info → A Personal Access Token (PAT) can be used instead.

         To create a PAT, visit https://app.docker.com/settings
Password: 


webhook payload url grok

brew install ngrok

ngrok config add-authtoken 3AtYKaMTqal4F2ska5U9dCNz8b1_3TsS9sn5N2wwqzN75pG8K

ngrok http 8080


https://sindy-touristy-emersyn.ngrok-free.dev/github-webhook/

-----------------------------------
Html 
brew update
brew install nginx

brew services start nginx

http://localhost:8081


<!DOCTYPE html>
<html>
<head>
    <title>My First Web Page</title>
</head>
<body>

    <h1>Hello World</h1>
    <p>This page is running inside Docker + Nginx</p>

</body>
</html>

Save as index.html

Dockerfile


FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;”]



nginx download

docker build -t myapp .

docker run -p 8081:80 myapp


http://localhost:8081

Java
public class App {
    public static void main(String[] args) {
        System.out.println("Hello from Java inside Docker 🚀");
    }
}

FROM eclipse-temurin:17

WORKDIR /app

COPY app.java .

RUN javac app.java

CMD ["java", "app”]


docker build -t java-app .
docker run java-app

change name tagnname build name for everyfile
