pipeline { 
agent any
    stages { 
        stage ('Build') {
            steps {
                sh 'docker image build -t flask_docker .  '
            }
        }
        stage ('Test') {
            steps {
                echo 'testing file'
                script {
                    try {
                    sh 'python test.py'
                    }
                    catch (err) {
                        echo err
                    }
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