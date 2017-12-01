pipeline {
  agent none
  stages {
	stage('Unit Test') {
	  agent {
		label 'build' 
	  }
      steps {
        deleteDir()
		echo 'Unit Test here'
      }
    }
    stage('Build Package') {
      agent {
        label 'build' 
      }      
      steps {
        deleteDir()
		echo 'Build Package here'
        sh '''
        whoami
        pwd
        export PATH="/home/jenkins/.pyenv/bin:$PATH"
        which pyenv
        pyenv init -
        pyenv virtualenv-init -

        pyenv versions
        pyenv install -s 3.6.3 || true
        pyenv global 3.6.3
        pyenv versions
        pip install wheel || true

        cd MyApplication
        python --version
        python setup.py sdist
        python setup.py bdist_wheel
'''
        archiveArtifacts 'MyApplication/dist/*'
        stash includes: 'MyApplication/dist/', name: 'package'
      }
    }
    stage('Install package') {
      agent {
        label 'install' 
      }
      steps {
        echo 'install package here'
        unstash 'package'
        sh '''
        export PATH="/home/jenkins/.pyenv/bin:$PATH"
        which pyenv
        pyenv init -
        pyenv virtualenv-init -

        pyenv versions
        pyenv install -s 3.6.3 || true
        pyenv global 3.6.3
        pyenv versions
        pip install wheel || true
        
        pip install MyApplication/dist/*.whl
        
        '''
      }
    }
  }
}
