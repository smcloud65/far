node {
        
        stage('Clone repository') {
            checkout scm
        }

        stage('Fargate Task call') {
                sh 'curl -s -k -u ci2:P@ssw0rd https://tr01.westus.cloudapp.azure.com/api/v1/defenders/fargate.json?consoleaddr=https://tr01.westus.cloudapp.azure.com -X POST -H "Content-Type:application/json" --data-binary "@fargate.json" | jq . > fargateAWS.json'
                sh 'cat fargateAWS.json'
        }

        stage('Publish Function') {
                sh 'aws ecs register-task-definition --cli-input-json file://fargateAWS.json'
                sh 'aws ecs update-service --cluster FargateCluster --service fargateappservice --task-definition fargatetaskdef:4 --desired-count 1'
        }
    }
