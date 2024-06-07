def registry = 'https://namln.jfrog.io/'
def imageName = 'namln.jfrog.io/valaxy-docker-local/ttrend'
def version   = '2.1.3'
pipeline{
    agent any
    // agent {
    //     node {
    //         label 'maven'
    //     }
    // }
    // environment {
    // PATH = "/usr/share/apache-maven/bin:$PATH"
    // }
    // stages{
    //     stage('Clone Code from Git'){
    //         steps{
    //             git branch: 'main', url: 'https://github.com/namkattor123/CI-CDpipelines.git'
    //         }
    //     }
    //     stage("Build"){
    //         steps {
    //              echo "----------- build started ----------"
    //             sh 'mvn clean deploy -Dmaven.test.skip=true'
    //              echo "----------- build complted ----------"
    //         }
    //     }
    //     stage("Test"){
    //         steps{
    //             echo "----------- unit test started ----------"
    //              echo "----------- unit test Complted ----------"
    //         }
    //     }
    //     stage('SonarQube analysis') {
    //         environment{
    //             scannerHome = tool 'namln-sonar-scanner';
    //         }
    //         steps{
    //             withSonarQubeEnv('namln-sonarquebe-server') { 
    //             sh "${scannerHome}/bin/sonar-scanner"
    //         }
    //         }
    //     }
    //     stage("Jar Publish") {
    //         steps {
    //             script {
    //                     echo '<--------------- Jar Publish Started --------------->'
    //                     def server = Artifactory.newServer url:registry+"/artifactory" ,  credentialsId:"0808095f-27f3-47f2-b89f-1ba29f48f28d"
    //                     def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
    //                     def uploadSpec = """{
    //                         "files": [
    //                             {
    //                             "pattern": "jarstaging/(*)",
    //                             "target": "libs-release-local/{1}",
    //                             "flat": "false",
    //                             "props" : "${properties}",
    //                             "exclusions": [ "*.sha1", "*.md5"]
    //                             }
    //                         ]
    //                     }"""
    //                     def buildInfo = server.upload(uploadSpec)
    //                     buildInfo.env.collect()
    //                     server.publishBuildInfo(buildInfo)
    //                     echo '<--------------- Jar Publish Ended --------------->'  
                
    //             }
    //         }   
    //     }   
        stage(" Docker Build ") {
            steps {
                script {
                echo '<--------------- Docker Build Started --------------->'
                app = docker.build(imageName+":"+version)
                echo '<--------------- Docker Build Ends --------------->'
                }
            }
        }

        stage (" Docker Publish "){
            steps {
                script {
                echo '<--------------- Docker Publish Started --------------->'  
                    docker.withRegistry(registry, '0808095f-27f3-47f2-b89f-1ba29f48f28d'){
                        app.push()
                    }    
                echo '<--------------- Docker Publish Ended --------------->'  
                }
            }
        }
    //     stage (" Deploy on K8S "){
    //         steps {
    //             script {
    //             echo '<--------------- Start Deploy --------------->' 
    //                 sh 'chmod +x deploy.sh' 
    //                 sh'./deploy.sh'   
    //             echo '<--------------- End Deploy --------------->'  
    //             }
    //         }
    //     }
    // }
}
