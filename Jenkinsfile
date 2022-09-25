node {
     docker.image('maven:3.8.1-adoptopenjdk-11').inside('-v /root/.m2:/root/.m2') {
        checkout scm
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk menlanjutkan)'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sleep(time: 60, unit: "SECONDS")
        }	
    }
}