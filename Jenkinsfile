
pipeline {
    
    environment {
    imagename = "becomedevops/petclinics"
    registryCredential = 'mydockercredentials'
    dockerImage = ''
  }
    agent any

    stages {
        
        
        
        stage('git') {
            steps {
                echo 'clonning Repository'
                git branch: 'main', url: 'https://github.com/mnagen/spring-petclinic.git'
                
                echo 'Repo clone successfully'
            }
            
        }
        
        
       stage('build') {
            steps {
                echo 'Build the code'
                sh './mvnw package'
            }
       }
            
            
            
            
            stage('DOCKERIZE') {
            steps {
                echo 'Deploy the code'
                
                script {
                    
                     dockerImage = docker.build imagename 
                    
                }
                  
                
            } 
                
            }  
            
            
            stage('push') {
            steps {
                echo 'push image'
                script{
                    
                 docker.withRegistry( '', registryCredential ) {
                  dockerImage.push("$BUILD_NUMBER")
                  dockerImage.push('latest')
                 }}

          }
                
                
                
                
            }
        
        
        
        
        
        stage('Remove Unused docker image') {
steps{
sh "docker rmi $imagename:$BUILD_NUMBER"
sh "docker rmi $imagename:latest"
    
    
}}
        } 
        
        
        
        
        
        
        
    }
    
    

