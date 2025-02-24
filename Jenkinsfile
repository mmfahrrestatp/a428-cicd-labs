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
            sh './jenkins/scripts/deliver.sh'
            sleep time: 1, unit: 'MINUTES'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}