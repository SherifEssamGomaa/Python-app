pipeline {
    agent any
    stages {
        stage('CI') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                    sh """
                        docker build . -t sherifessamgomaa/python-app:v$BUILD_NUMBER
                        docker login -u ${USERNAME} -p ${PASSWORD}
                        docker push sherifessamgomaa/python-app:v$BUILD_NUMBER
                    """
                }
            }
            post {
                success {
                    echo "success"
                }
                failure {
                    echo "failure"
                }
            }
        }

        stage('CD') {
            steps {
                withCredentials([file(credentialsId: 'service-account-credentials', variable: 'config')]){
                    sh """
                        gcloud auth activate-service-account --key-file=${config}
                        gcloud container clusters get-credentials cluster --zone us-east4-b --project iti-sherif
                        sed -i 's/tag/${BUILD_NUMBER}/g' Kubernetes/kubernetes.yaml
                        kubectl apply -Rf Kubernetes
                    """
                }
            }
            post {
                success {
                    echo "success"
                }
                failure {
                    echo "failure"
                }
            }
        }

    }
}