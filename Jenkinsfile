pipeline{
    
    agent any 
    tools {
     maven 'maven-3.9.1'
    }
    
    
    stages{
        stage ('checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/zielotechgroup/maven-standalone-app.git'
            }
        }
        
        stage ('Build') {
            steps{
                sh 'mvn clean package'
            }
        }
        
         stage ('Test') {
            steps{
                sh 'mvn test'
            }
        }
        
          stage ('Code quality analysis') {
            steps{
                sh 'mvn checkstyle:checkstyle'
                recordIssues(tools: [checkStyle()])
            }
        }
        
           stage ('Code coverage') {
            steps{
                jacoco maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
            }
        }
        
         stage ('Docker Build and Publish') {
            steps{
                // sh 'docker build -t web .'
                
                withCredentials([usernamePassword(credentialsId: 'Docker_cred_new', passwordVariable: 'passwd', usernameVariable: 'uname')]) {
                sh 'docker login -u $uname -p $passwd'
                    // some block
                sh 'docker tag web:latest amahalankar2/demo123:v3'
                sh 'docker push amahalankar2/demo123:v3'
                }
               
            }
        }
    }
}
