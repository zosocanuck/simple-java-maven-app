pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Venafi') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install --no-install-recommends -y wget ca-certificates'
                sh 'wget https://vh.venafidemo.com/csc/clients/venafi-csc-latest-x86_64.deb'
                sh 'dpkg -i venafi-csc-latest-x86_64.deb'
            }
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
