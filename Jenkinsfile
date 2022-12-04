pipeline {
    agent any
    
    environment{
        registry= "toncheto/javaapp"
        registryCredential = 'dockerhub_id'
        
    }
    
    stages {
        stage('Info') {
            steps {
                sh '''
                echo "Displaying some info about the agent"
                whoami
                id
                docker ps
                echo "worspace: ${WORKSPACE}"
                #rm -rf "${WORKSPACE}"/target && mkdir "${WORKSPACE}"/target
                #touch "${WORKSPACE}"/target/test.jar
                '''
            }
        }
        stage('Build') {
            agent {
                docker { image 'maven:3.8.1-adoptopenjdk-11' }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
            post {
              success {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
              }
            }
        }
//         stage('Test') {
//             agent {
//                 docker { image 'maven:3.8.1-adoptopenjdk-11' }
//             }            
//             steps {
//                 sh 'mvn test'
//             }
//             post {
//                 always {
//                     junit 'target/surefire-reports/*.xml'
//                 }
//             }
//         }
        stage('Build Docker image') {
            agent {
                docker { image 'docker:20.10.21-alpine3.17' }            
            }
            
            steps {
                sh '''
                docker build -t "$registry:$BUILD_NUMBER" --build-arg WORKSPACE="${WORKSPACE}" .
                echo "Listing all images:"
                docker images
                '''
            }
        }
        stage('Completed') {
            steps {
                echo 'Job completed'
            }
        }        
    }
}
