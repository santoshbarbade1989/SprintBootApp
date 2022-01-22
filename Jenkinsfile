pipeline{
    agent{
        label "aws_node"
    }
    tools{
        maven 'sbbMaven' 
    }
    stages{
        stage("Test"){
            steps{
                sh "mvn --version"
                sh 'mvn test'
            }  
        }
        stage("SonarQube"){
            steps{
             
                sh 'mvn sonar:sonar'
            }  
        }
        stage("Build"){
            steps{
                sh 'mvn package'
            }  
        }
        stage("Deploy"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '61f40ece-d988-4ed8-869f-5292560be868', path: '', url: 'http://54.152.32.154:8080/')], contextPath: 'nodeCommand', war: '**/*.war'
            }  
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
