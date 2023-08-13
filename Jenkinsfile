pipeline {
    agent any
    stages{
        stage("Checkout"){
            steps{
                git branch: 'main',
                url : 'https://github.com/puneet785/pipelines-java.git'

            }
        }

        stage("Build"){
            steps{
            sh "mvn package"
            }
        }

        stage("Install"){
            steps{
            sh "mvn install"
            }
        }
        
        stage('Deploy'){
            steps{
                echo "Deploy stage"
                deploy adapters: [tomcat9 (
                       credentialsId: 'tomcat_credential',
                       path: '',
                        url: 'http://52.168.4.168:8088/',
                )],
                contextPath: 'heypuneet',
                onFailure: 'false',
                var: '**/*.war'
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.war'
                }
            }
        }
    }
 
}
