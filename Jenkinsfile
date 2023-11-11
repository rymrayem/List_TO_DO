pipeline {
    agent any
    environment {
        
        DOCKERHUB_CREDENTIALS = credentials('rymkrayem')
    }
    stages {
        stage('Checkout'){
            agent any
            steps{
                
                git branch: 'main', url:'https://github.com/rymrayem/List_TO_DO.git'
            }
        }
        stage('Init'){
            steps{
                
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build'){
            steps {
                
               sh 'docker build -t rymkrayem/todo-list-app:$BUILD_ID -f ./Dockerfile .'
          
            }
        }
        stage('Deliver'){
            steps {
                
                sh 'docker push rymkrayem/todo-list-app:$BUILD_ID'
            }
        }
        stage('Cleanup'){
            steps {
            
            sh 'docker rmi rymkrayem/todo-list-app:$BUILD_ID'
            sh 'docker logout'
            }
        }
    }
}