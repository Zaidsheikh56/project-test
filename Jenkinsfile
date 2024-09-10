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
    stage('Code quality Analysis') {
      steps{
        sh'''
        sudo docker pull sonarqube
        sudo docker network create my-network4
        sudo docker run -d --name my-container-db1 --network my-network4 -e POSTGRES_USER=sonar -e POSTGRES_PASSWORD=sonar -e POSTGRES_DB=sonar postgres:9.6
        sudo docker run -d --name my-conatiner1 -p 9000:9000 --network my-network4 -e SONARQUBE_JDBC_URL=jdbc:postgresql://sonar-db:5432/sonar -e SONAR_JDBC_USERNAME=sonar -e SONAR_JDBC_PASSWORD=sonar sonarqube
        sudo cd /var/lib/jenkins/workspace/project-test/ && mvn sonar:sonar  -Dsonar.host.url=http://18.191.73.225:9000 -Dsonar.login=[sqa_218ec123c5a2edc8df58bbad52f2a72023903a68]
        '''
      }
    }
  }
}
