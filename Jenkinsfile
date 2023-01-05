
pipeline {
    agent any

    stages {
        stage('git download') {
            steps {
                
            }
        }
      
        stage('sending file') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync  -avh /var/lib/jenkins/workspace/dockerci/Dockerfile root@52.204.231.80:/root/dockerci/', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
      
        stage(' build dcker file') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /root/dockerci/
docker build -t $JOB_NAME:v$BUILD_ID .
docker tag  $JOB_NAME:v$BUILD_ID  amit1300/$JOB_NAME:v$BUILD_ID 
docker tag  $JOB_NAME:v$BUILD_ID  amit1300/$JOB_NAME:latest 

docker push  amit1300/$JOB_NAME:v$BUILD_ID 
docker push amit1300/$JOB_NAME:latest
docker rmi -f amit1300/$JOB_NAME:latest $JOB_NAME:v$BUILD_ID amit1300/$JOB_NAME:v$BUILD_ID ''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
      
      
        stage('playbook') {
            steps {
        sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /root/project/
ansible-playbook playbook.yaml''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
      
    }
}
