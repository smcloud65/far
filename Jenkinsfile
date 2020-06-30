node {
    
    stage('Clone repository') {
        checkout scm
    }

    stage('Fargate Task call') 
         {
            sh 'curl -s -k -u ci2 - p P@ssw0rd https://tr01.westus.cloudapp.azure.com/api/v1/defenders/fargate.json?consoleaddr=tr01.westus.cloudapp.azure.com -X POST -H "Content-Type:application/json" --data-binary "@fargate.json" | jq . > tw_fargate.json'
            sh 'cat tw_fargate.json'
        }
    

    stage('Publish Function') {
        archiveArtifacts artifacts: 'tw_fargate.json'}
}
