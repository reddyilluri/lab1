pipeline {
environment {
registry = "reddyilluri/hello-world"
registryCredential = 'reddyilluri'
dockerImage = 'golang:1.14'
}
agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/reddyilluri/lab1.git'
}
}
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}
