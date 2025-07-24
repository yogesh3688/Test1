    pipeline{

    agent any

    stages {

        stage('Start Grid'){
            steps {
                echo "Start Grid triigred"
                sh "docker compose -f grid.yaml up -d"
            
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
            sh "docker compose -f grid.yaml down"
            sh "docker compose -f test-suites.yaml down"
        }
    }
    }
