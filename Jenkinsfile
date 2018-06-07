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
stage('Shell Script Run') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Stage'
        }

      }
      steps {
        sh '''npm install
npm run build'''
      }
    }

    stage('Test') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh 'npm run test'
      }
    }
    stage('Deploy') {
      when {
        expression {
          params.REQUESTED_ACTION == 'Build'
        }

      }
      steps {
        sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
cd playbooks
ansible-playbook deploy_dev.yml
'''
      }
    }
  }
  parameters {
    choice(name: 'REQUESTED_ACTION', choices: '''Build
Stage''', description: 'Type of action to perform')
  }
}
