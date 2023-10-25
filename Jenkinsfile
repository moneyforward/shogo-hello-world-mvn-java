pipeline {
    agent any
    // tools{
    //     maven 'maven'
    // }
    environment {
   NEXUS_VERSION = "nexus3"
   NEXUS_PROTOCOL = "http"
   NEXUS_URL = "13.233.88.65:8081"
   NEXUS_REPOSITORY = "helloworld-app"
   NEXUS_CREDENTIAL_ID = "nexus"
   NEXUS_USERNAME= "admin"
   NEXUS_PASSWORD= "Sagar@123"
}

    // stages {
    //     stage('git checkout') {
    //         steps {
    //             git branch: 'main' , url:'https://github.com/gowdasagar06/hello-world-mvn-java.git'
    //         }
    //     }
    //     stage('build') {
    //         steps {
    //             withSonarQubeEnv('sonar'){
    //                 withMaven{
    //                     sh '/usr/bin/mvn clean verify sonar:sonar -Dsonar.javaOpts="-Xmx2g"'
    //                 }
    //             }
    //         }
    //     }
    //     stage('Quality Gate'){
    //         steps{
    //             timeout(time: 5, unit: 'MINUTES'){
    //             waitForQualityGate abortPipeline: true
    //             }
    //         }
    //     }
    //     stage("Publish to Nexus Repository Manager"){
    //         steps{
    //             script{
    //                  pom = readMavenPom file: "pom.xml";
    //                  filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
    //                  echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
    //                  artifactPath = filesByGlob[0].path;
    //                  artifactExists = fileExists artifactPath;
    //                  if(artifactExists){
    //                      echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
    //                      nexusArtifactUploader(
    //                           nexusVersion: NEXUS_VERSION,
    //                           protocol: NEXUS_PROTOCOL,
    //                           nexusUrl: NEXUS_URL,
    //                           groupId: pom.groupId,
    //                           version: pom.version,
    //                           repository: NEXUS_REPOSITORY,
    //                           credentialsId: NEXUS_CREDENTIAL_ID,
    //                           artifacts:[
    //                               [
    //                                   artifactId: pom.artifactId,
    //                                   classifier: '',
    //                                   file: artifactPath,
    //                                   type: pom.packaging
    //                                   ],
    //                                   [
    //                                       artifactId: pom.artifactId,
    //                                       classifier: '',
    //                                       file: "pom.xml",
    //                                       type: "pom"
    //                                       ]
    //                               ]
    //                          );
    //                  }else{
    //                      error "*** File: ${artifactPath}, could not be found";
    //                  }
                      
    //             }
    //         }
    //     } 
        stage('get war file'){
            steps{
                sh '''cd /var/lib/jenkins/workspace/
                
                sudo wget --user={$NEXUS_USERNAME} password={$NEXUS_PASSWORD} http://{$NEXUS_URL}/repository/{$NEXUS_REPOSITORY}/com/efsavage/{$pom.artifactId}/{$pom.version}/{$pom.artifactId}-{$pom.version}.war'''
            }
        }
        stage('build image'){
            steps{
                sh '''cd /var/lib/jenkins/workspace/
                      sudo docker build -t java_app -f tomcat.Dockerfile .
                '''
            }
        }
        stage('deploy'){
            steps{
                sh '''
                      sudo docker run -d --name tomcat -p 8082:8080 java_app
                '''
            }
        }
    }
}
