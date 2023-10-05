pipeline{
    agent{
        node{
            label 'maven'
        }    
    }
    stages{
        stage('Clone Code form Git'){
            steps{
                git branch: 'main', url: 'https://github.com/namkattor123/CI-CDpipelines.git'
            }
        }
    }
}