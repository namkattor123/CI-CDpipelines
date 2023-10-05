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
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                 echo "----------- unit test Complted ----------"
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
        def registry = 'https://namln.jfrog.io/'
        stage("Jar Publish") {
        steps {
            script {
                    echo '<--------------- Jar Publish Started --------------->'
                     def server = Artifactory.newServer url:registry+"/artifactory" ,  credentialsId:""
                     def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                     def uploadSpec = """{
                          "files": [
                            {
                              "pattern": "jarstaging/(*)",
                              "target": "libs-release-local/{1}",
                              "flat": "false",
                              "props" : "${properties}",
                              "exclusions": [ "*.sha1", "*.md5"]
                            }
                         ]
                     }"""
                     def buildInfo = server.upload(uploadSpec)
                     buildInfo.env.collect()
                     server.publishBuildInfo(buildInfo)
                     echo '<--------------- Jar Publish Ended --------------->'  
            
            }
        }   
    }   
    }
}
