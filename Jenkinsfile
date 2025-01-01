pipeline {
    agent {
        docker {
            image 'alpine:latest'
            args '-u 0:0' // Run the container as root
        }
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                # Install Python and pip
                apk add --no-cache python3 py3-pip
                
                # Create and activate a virtual environment
                python3 -m venv venv
                . venv/bin/activate
                
                # Verify Python and pip versions in the virtual environment
                python --version
                pip --version
                
                # Navigate to the app directory and install dependencies
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                # Activate the virtual environment
                . venv/bin/activate
                
                # Navigate to the app directory and run tests
                cd myapp
                python hello.py
                python hello.py --name=Brad
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "Doing delivery stuff.."
                '''
            }
        }
    }
}
