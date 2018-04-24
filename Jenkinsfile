properties([pipelineTriggers([githubPush()])])
node('linux') {
    git url: 'https://github.com/rclc/infrastructure-pipeline.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
    
    stage ("GetInstances") {

        sh "aws ec2 describe-instances --region us-east-1"
    }

    stage("CreateInstance") {
        sh "aws ec2 run-instances --image-id ami-467ca739 --count 1 --instance-type t2.micro --key-name SEIS665-demo --security-group-ids sg-0fc84e78 --region us-east-1"
    }
    
    stage("TerminateInstance") {
       sh "aws ec2 describe-instances --region us-east-1 | jq ." 
       def output = sh returnStdout: true, script: 'aws ec2 describe-instances --region us-east-1 | jq .'
       sh "aws ec2 wait instance-running --instance-ids $output"
       sh "aws ec2 terminate-instances --instance-ids $output"
    }
    
}
