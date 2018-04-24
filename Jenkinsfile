properties([pipelineTriggers([githubPush()])])
node('linux') {
    git url: 'https://github.com/rclc/infrastructure-pipeline.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
    
    stage ("GetInstances") {

      sh "aws ec2 describe-instances --region us-east-1"
    }

    stage ("CreateInstance") {
   
      sh "aws ec2 run-instances --image-id ami-287dnf7 --count 1 --instance-type t2.micro --key-name seis665 --security-group-ids sg-7edf3108 --subnet-id subnet-0bbd366e --region us-east-1"
    }
    
    
}
