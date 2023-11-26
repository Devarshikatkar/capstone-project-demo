node{
    
    stage('code checkout'){
        git 'https://github.com/Devarshikatkar/capstone-project-demo.git'
    }
    
    stage('code build'){
        sh 'mvn clean package'
        
    }
    stage('containerize'){
        sh 'docker build -t devarshikatkar/insure-me:1.0 .'
        
    }
    stage('push to dockerhub '){
        
        withCredentials([string(credentialsId: 'dockerPwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u devarshikatkar -p ${'dockerHubPwd'}"
        sh 'docker push devarshikatkar/insure-me:1.0 .'}
    }
        
    stage('deploy')
        ansiblePlaybook become: true, credentialsId: 'ansible-ssh-jenkins-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts/', playbook: 'configure-test-server.yml'
        
        
        
    }
