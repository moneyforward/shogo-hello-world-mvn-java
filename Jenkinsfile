pipeline{
    agent any
    tools{
        git 'Default'
        maven 'maven'
    }
    stages{
        stage("build"){
            steps{
                sh 'mvn clean package'
            }
        }
    }
}
