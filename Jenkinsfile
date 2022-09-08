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
                sh '''#!/bin/bash
                       apt-get update
                       apt-get install --no-install-recommends -y wget ca-certificates
                       wget https://vh.venafidemo.com/csc/clients/venafi-csc-latest-x86_64.deb
                       dpkg -i venafi-csc-latest-x86_64.deb
                   '''
            }
        }
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
