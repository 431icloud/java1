pipeline {
    agent any
    stages {
        stage ('Continous Download') 
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage ('Continous Build') 
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage ('Continous Development') 
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'd3b2a2b7-e309-4b06-8969-98b48f1e28a7', path: '', url: 'http://172.31.33.252:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage ('Continous Testing') 
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/JAVA/testing.jar'
            }
        }
        stage ('Continous Delivery') 
        {
            steps
            {
                input message: 'need approval form DM', submitter: 'admin'
                deploy adapters: [tomcat9(credentialsId: 'd3b2a2b7-e309-4b06-8969-98b48f1e28a7', path: '', url: 'http://172.31.43.146:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
       
    }
}
