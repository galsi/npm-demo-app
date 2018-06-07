pipeline {
  agent any
  stages {
    stage('Shell Script Run') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh '''npm install
npm run build'''
      }
    }
    stage('Test') {
      steps {
        sh 'npm run test'
      }
    }
    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
cd playbooks
ansible-playbook deploy_dev.yml
'''
          }
        }
        stage('Uplad') {
          steps {
            sh 'curl -uadmin:APBcyn5vVoefw71T -T nodejs-demoapp.zip "http://35.205.54.43:8081/artifactory/generic-local/nodejs-demoapp.zip"'
          }
        }
      }
    }
  }
  parameters {
    choice(name: 'REQUESTED_ACTION', choices: '''Build
Stage''', description: 'Type of action to perform')
  }
}