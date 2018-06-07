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
      steps {
        sh '''mkdir playbooks/files
cp nodejs-demoapp.zip playbooks/files/nodejs-demoapp.zip
ansible-playbook playbook/deploy_dev.yml
'''
      }
    }
  }
  parameters {
    choice(name: 'REQUESTED_ACTION', choices: '''Build
''', description: 'Type of action to perform')
  }
}