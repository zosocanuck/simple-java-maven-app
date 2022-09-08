pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11' 
            args '-u root -v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Venafi') {
            steps {
                sh '''#!/bin/bash
                       apt-get update
                       apt-get install --no-install-recommends -y wget ca-certificates
                       wget https://vh.venafidemo.com/csc/clients/venafi-csc-latest-x86_64.deb
                       wget https://vh.venafidemo.com/poc_guide/venafipkcs11.txt -O /root/venafipkcs11.txt
                       dpkg -i venafi-csc-latest-x86_64.deb
                       /opt/venafi/codesign/bin/pkcs11config getgrant --force --authurl=https://vh.venafidemo.com/vedauth --hsmurl=https://vh.venafidemo.com/vedhsm --username=sample-cs-user --password=Passw0rd123!
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
