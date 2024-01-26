node {
    docker.image ('maven:3.9.0') .inside('-v /root/.m2:/root/.m2') {

        stage ('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        
        stage ('Test') {
            try {
                sh 'mvn test'
            }
            catch (Exception e) {
                currentBuild.result='FAILURE'
            }
            finally {
                junit 'target/surefire-reports/*.xml'
            }
        }

        stage ('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy? (klik "proceed" untuk melanjutkan)'
        }

        stage ('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sleep (time: 60, unit: 'SECONDS')
        }
    }
}