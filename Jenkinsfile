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
        stage('SonarQube analysis') {
            environment{
                scannerHome = tool 'namln-sonar-scanner';
            }
            steps{
                withSonarQubeEnv('namln-sonarquebe-server') { 
                sh "${scannerHome}/bin/sonar-scanner"
            }
            }
        }
    }
}
0ee8e4b146e32f2d9e71ab62875303cdb1bb5f01