node {
        
        stage('Clone repository') {
            checkout scm
        }

        stage('Fargate Task call') {
                sh 'curl --progress-bar -L -k --header "authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiYWRtaW4iLCJyb2xlIjoiYWRtaW4iLCJncm91cHMiOm51bGwsInNlc3Npb25UaW1lb3V0U2VjIjoxODAwLCJleHAiOjE1OTM0OTU4NjAsImlzcyI6InR3aXN0bG9jayJ9.Y5YSVq5Seic1731Qj2tptA0eVraTeXIszekrjDNG_SI" https://tr01.westus.cloudapp.azure.com/api/v1/defenders/fargate.json?consoleaddr=https://tr01.westus.cloudapp.azure.com -X POST -H "Content-Type:application/json" --data-binary "@fargate.json" | jq . > fargateAWS.json'
                sh 'cat fargateAWS.json'
        }

        stage('Publish Function') {
                sh 'aws ecs register-task-definition --cli-input-json file://fargateAWS.json'
                sh 'aws ecs update-service --cluster FargateCluster --service fargateappservice --task-definition fargatetaskdef:4 --desired-count 1'
        }
    }
