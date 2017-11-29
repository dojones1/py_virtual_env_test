Sample package process built using instructions from:
https://www.digitalocean.com/community/tutorials/how-to-package-and-distribute-python-applications
https://packaging.python.org/tutorials/distributing-packages/#uploading-your-project-to-pypi

To install virtual environment package:
sudo apt-get install -y python3-pip
sudo pip3 install pip
sudo pip3 install --upgrade virtualenv
sudo pip3 install --upgrade virtualenvwrapper

To setup virtual environment
Add to .bashrc:
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Devel
source /usr/local/bin/virtualenvwrapper.sh


To build package:
cd ~/MyApplication
python setup.py sdist
python setup.py bdist_wheel

dist folder will contain:
- Resultant *.tar.gz file
- Resultant *.whl file

Store the file as an artifact

To install at the destination:
pip install <file>.tar.gz
or pip install <file>.whl
