pipeline{
    agent {
        node {
            label 'maven'
        }
    }
    environment {
    PATH = "/usr/share/apache-maven/bin:$PATH"
    }
    stages{
        stage('Clone Code from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/namkattor123/CI-CDpipelines.git'
            }
        }
        stage("build"){
            steps {
                 echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                 echo "----------- build complted ----------"
            }
        }
    }
}
