pipeline{
    agent any
    tools{
        git 'Git'
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
