pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                echo "make"
            }
        }
        stage('Test'){
            steps{
                echo "make check || true"
            }
        }
        stage('Deploy'){
            steps{
                echo "make publish"
            }
        }
    }
}