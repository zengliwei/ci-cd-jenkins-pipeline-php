pipeline {
    stages {
        stage('Build') {
            agent {
                node {
                    label 'staging'
                    customWorkspace '/var/www/current/jenkins/test'
                }
            }
            steps {
                checkout(
                    [
                        $class: 'GitSCM',
                        userRemoteConfigs: [[url: 'https://github.com/zengliwei/ci-cd-jenkins-pipeline-php']],
                        branches: [[name: '*/main']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [],
                        submoduleCfg: []
                    ]
                )
                sh 'composer install'
            }
        }
        stage('Test') {
            agent {
                node {
                    label 'staging'
                    customWorkspace '/var/www/current/jenkins/test'
                }
            }
            steps {
                sh 'vendor/phpunit/phpunit/phpunit -c ci-cd/phpunit.xml'
            }
        }
    }
}
