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
                sh 'pip3 install flask'
                sh 'pip3 install virtualenv'
                sh 'virtualenv flask'
                sh 'cd flask'
                sh 'source bin/activate'
                sh 'pip install flask'
                sh 'python3 test.py'
                input(id: "Deploy Gate", message: "Deploy ${params.project_name}?", ok: 'Deploy')
            }

        }
        stage ('Deploy') {
            steps{
                echo 'Deployed'
            }
        }
 
    }           
 }