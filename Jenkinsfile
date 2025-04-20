pipeline {
    agent none

    stages {
        stage("Continuous Integration / Intégration Continue") {
            agent { label "${AGENT_COMPOSER}" }
            steps {
                git branch: "main", url: "https://github.com/ABoudjemaa/symfony_CICDCD"
                sh "composer install"
            }
        }
        stage("Continuous Delivery / Livraison Continue") {
            agent { label "${AGENT_DOCKER}" }
            steps {
                sh "docker build . -t ${DOCKERHUB_USERNAME}/next_cicdcd"
                sh "docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKER_PASSWORD}" // Créer un PAT sur Docker Hub : https://app.docker.com/settings/personal-access-tokens
                sh "docker push ${DOCKERHUB_USERNAME}/next_cicdcd"
            }
        }
    }
}