pipeline {
  agent {
    label 'ubuntu' 
  }
  stages {
    stage('Unit Test') {
      steps {
        echo 'Unit Test here'
      }
    }
    stage('Build Package') {
      steps {
        echo 'Build Package here'
        sh '''whoami
        pwd
        curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
export PATH="/var/lib/jenkins/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

pyenv versions
pyenv install 3.6.3 || true
pyenv global 3.6.3
pyenv versions
pip install wheel || true

cd MyApplication
python --version
python setup.py sdist
python setup.py bdist_wheel

'''
        archiveArtifacts 'MyApplication/dist/*'
      }
    }
    stage('Install package') {
      steps {
        echo 'install package here'
      }
    }
  }
}
