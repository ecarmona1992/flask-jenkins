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
                sh "pip3 install -r requirements.txt"
                sh 'python3 -m pytest test.py'
                // input(id: "Deploy Gate", message: "Deploy ${params.project_name}?", ok: 'Deploy')
            }

        }
        stage ('Deploy') {
            steps{
                echo 'Deployed'
            }
        }
 
    }           
 }