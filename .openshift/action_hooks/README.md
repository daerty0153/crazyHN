#!/bin/bash
# This deploy hook gets executed after dependencies are resolved and the
# build hook has been run but before the application has been started back
# up again.  This script gets executed directly, so it could be python, php,
# ruby, etc.
 
source ${OPENSHIFT_HOMEDIR}python-2.6/virtenv/bin/activate
 
export PYTHON_EGG_CACHE=${OPENSHIFT_HOME_DIR}python-2.6/virtenv/lib/python-2.6/site-packages
 
echo "Executing 'python ${OPENSHIFT_REPO_DIR}mywebsite/manage.py syncdb --noinput'"
python "$OPENSHIFT_REPO_DIR"mywebsite/manage.py syncdb --noinput
 
echo "Executing 'python ${OPENSHIFT_REPO_DIR}mywebsite/manage.py collectstatic --noinput -v0'"
python "$OPENSHIFT_REPO_DIR"mywebsite/manage.py collectstatic --noinput -v0
