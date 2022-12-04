pipeline {
    agent any
//     agent {                
//         docker {
//             image 'toncheto/jenkins-agent-git-docker:3'
//             args '-v /var/run/docker.sock:/var/run/docker.sock'
//             }
//         }            
    
    environment{
        registry= "toncheto/javaapp"
        registryCredential = 'dockerhub_id'
        
    }
    
    stages {           
        stage('Info') {
//         agent {                
//             docker {
//                 image 'toncheto/jenkins-agent-git-docker:3'
//                 args '-v /var/run/docker.sock:/var/run/docker.sock'
//             }
//         }               
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
                docker { 
                    image 'maven:3.8.1-adoptopenjdk-11' 
                args '-v /root/.m2:/root/.m2'
                }
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
//             agent {                
//                 docker {
//                     image 'toncheto/jenkins-agent-git-docker:3'
//                     args '-v /var/run/docker.sock:/var/run/docker.sock'
//                 }
//             }             
            
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
