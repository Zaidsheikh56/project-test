pipeline {
  agent any
  stages {
    stage('git checkout')  {
      steps {
         git 'https://github.com/Pritam-Khergade/student-ui.git' 
      }
    }
    stage('build with maven') {
      steps {
        sh 'sudo yum update -y && sudo yum install maven -y && sudo mvn clean install'
      }
    }
    stage('docker build stage') {
      steps {
        sh'''
        sudo yum install docker -y && sudo systemctl enable --now docker 
        sudo docker build -t zaidsheikh5656/firstimage .
        sudo docker login -u zaidsheikh5656 -p zaidzimad12345
        sudo docker push zaidsheikh5656/firstimage
        '''
      }
    }
   
    stage('deploy to staging')  {
      steps{
        deploy adapters: [tomcat9(credentialsId: 'eefe689f-ef8f-473b-8533-a60d455615f3', path: '', url: 'http://172.31.16.41:8080')], contextPath: '/', war: '**/*.war'
      }
    }
  }
}
          

