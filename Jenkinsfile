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
    }
}