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
        sudo docker network create my-network5
        sudo docker run -d --name my-container-db3 --network my-network5 -e POSTGRES_USER=sonar -e POSTGRES_PASSWORD=sonar -e POSTGRES_DB=sonar postgres:9.6
        sudo docker run -d --name my-conatiner3 -p 9000:9000 --network my-network5 -e SONARQUBE_JDBC_URL=jdbc:postgresql://sonar-db:5432/sonar -e SONAR_JDBC_USERNAME=sonar -e SONAR_JDBC_PASSWORD=sonar sonarqube
        sudo cd /var/lib/jenkins/workspace/project-test/ && mvn sonar:sonar  -Dsonar.host.url=http://18.191.73.225:9000 -Dsonar.login=[sqa_ac5ca888ef75509845da23e2d3b21aa7482e24dd]
        '''
      }
    }
  }
}
