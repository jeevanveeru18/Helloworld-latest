pipeline {
    agent { label "project_slave" }
    
    triggers {
        pollSCM('* * * * *')
    }    

    stages {
        stage('clone_project_A') {
            steps {
                echo 'clone project A'
                git 'https://github.com/jeevanveeru18/Helloworld-latest.git'
            }
        }
        stage('build_project_A') {
            steps {
                echo 'build_projectA'
                sh 'yum install maven -y'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        } 
        stage('Docker_build') {
            steps {
                echo 'Docker build_projectd'
                sh 'docker build -t myproject .' 
            }
        }
        stage('login to dockerhub') {
            steps {
                echo 'login to dockerhub'
                sh 'docker login -u jeevanveeru18 -p Jeevan45$'
            }
        } 
        stage('Tag the Image') {
            steps {
                echo 'Tag the Image'
                sh 'docker tag  myproject jeevanveeru18/myproject'
            }
        } 
        stage('Deploy to docker hub') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker push jeevanveeru18/myproject '
            }
        }
        stage('Remove Docker conatiner') {
            steps {
                echo 'Remove Docker conatiner'
                sh 'docker stop myproject_conatiner || true'
                sh 'docker rm myproject_conatiner || true'
            }
        }        
        stage('Run docker image') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker run --name myproject_conatiner -d -p 8181:8080 jeevanveeru18/myproject'
            }
        }
        stage('added one more stage') {
            steps {
                echo 'added one more stage'                
            }
        }        
    }
}
