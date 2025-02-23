node {  
    /* Requires the Docker Pipeline plugin to be installed */
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            checkout scm
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: "Lanjutkan ke tahap Deploy?"
        }
        stage('Deploy') {
            sleep time: 1, unit: 'MINUTES'
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}