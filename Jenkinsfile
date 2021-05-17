pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                echo 'git checkout'
                // git credentialsId: '34361bfd-aa0f-4178-8b3d-8e09fe610d2b', url: 'https://github.com/ghUserMan/maven-java-sample-app.git'
            }
        }
        stage('build') {
            steps {
                echo 'build'
                sh 'mvn clean package'
            }
        }
        stage('archive') {
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                // archive 'target/*.jar'
                
                echo 'archive'
            }
            post {
              always {
                  junit 'target/surefire-reports/*.xml'
                // One or more steps need to be included within each condition's block.
              }
              success {
                // One or more steps need to be included within each condition's block.
                // archive 'target/*.jar'
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
              }
            }
        }
        stage('deploy') {
            steps {
                withEnv(['jENKINS_NODE_COOKIE=dontKillMe']) {
                    sh 'nohup java -jar -Dserver.port=8888 target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.jar &'
                }
            }
        }
    }
}

