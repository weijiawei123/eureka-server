
pipeline {
    agent any
    stages { 
        stage('Checkout') {
            steps {
                echo 'pull git'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-account', url: 'https://github.com/cweijiaweil-github/hellojib.git']]])
            }
        } 
        stage('Build') {
            steps {
                echo 'package'
                bat "mvn -Dmaven.test.failure.ignore clean package" 
            }
        }
        stage('Image') { 
            steps { 
                echo "Build To Docker!" 
                bat 'docker build -t eureka:v1 .' 
            } 
        }    
        stage('Run') { 
            steps { 
                echo "Run Docker Image" 
                bat 'docker run -d -p 9100:9100 eureka:v1' 
            } 
        }     
    }
}