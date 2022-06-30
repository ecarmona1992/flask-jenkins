pipeline { 
agent any 
    stages { 
        stage ('Build') {
            steps {
                echo 'Starting Build Phase'
                sh 'docker image build -t flask_docker .'
                echo 'Build Phase Completed'
            } 
 
        }
        stage ('Test') {
            steps {
                echo 'testing file'
                try {
                    sh 'python .\test.py'
                }
                catch (err) {
                    echo err
                }
            }

        }
        stage ('Deploy') {
            steps{
                sh 'docker run -p 5000:5000 -d flask_docker'
                echo 'Running on localhost:5000'
            }
        }
 
    }           
 }