    pipeline{

    agent any

    parameters {
  choice choices: ['firefox', 'chrome'], description: 'Select Browser', name: 'BROWSER'
}


    stages {

        stage('Start Grid'){
            steps {
                echo "Start Grid triigred"
                sh "docker compose -f grid.yaml up --scale ${params.BROWSER}=2  -d"
            
            }
        }

        stage('Run Test'){
            steps {
                sh "docker compose -f test-suites.yaml up"
            }
            
        }
        
    }

    post {
        always {
            echo "inside post always block"
            sh "docker ps"
            archiveArtifacts artifacts: 'output/yogesh-selenium-output/emailable-report.html',followSymlinks: false
            sh "docker compose -f grid.yaml down"
            sh "docker compose -f test-suites.yaml down"
        }
    }
    }
