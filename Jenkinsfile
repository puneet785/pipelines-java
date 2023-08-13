pipeline {
    agent any

 

    // tools {
    //     // Install the Maven version configured as "M3" and add it to the path.
    //     maven "M3"
    // }

 

    stages {
        stage('Checkout') {
            steps {
                
                git branch: 'main',
                url : 'https://github.com/puneet785/pipelines-java.git'
            }
        }
        stage('Build') {
            steps{
                  // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

 

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"

 

            }
        }
        stage('Deploy'){
            steps{
                echo "Deploy stage"
                deploy adapters: [tomcat9 (
                       credentialsId: 'tom_deployment',
                       path: '',
                       url: 'https://168.62.165.69:8080/'
                )],
                contextPath: 'helloworld',
                onFailure: 'false',
                war: '**/*.war'
            }
           
        }

    }
}
