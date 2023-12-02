if you have this folder structure:

* project_app_name/
	* management/
		* a_file_to_run.py
* webapps/
* manage.py
* script.py

then in script.py, you can run a command like this:
```python
import os
import subprocess
import sys
from threading import Thread
import datetime
import schedule
import time

def run_cmd(cmd):
    print("command runned -",cmd)
    print("iteeration - ",datetime.datetime.now())
    Thread(target = lambda x: subprocess.run(x,stdout = subprocess.PIPE,stderr=subprocess.STDOUT,shell=True) ,args = ([cmd])).start()
cmd = 'cd /var/www/webapps/project_app_name && python manage.py a_file_to_run > cronjobOutput_test.txt 2>&1'
schedule.every(15).minutes.do(run_cmd,cmd = cmd)

while True:
    schedule.run_pending()
    time.sleep(1)
```


focus on the `python manage.py a_file_to_run` part

such that a_file_to_run.py contains the following:

```python
from django.conf import settings
from django.core.management.base import BaseCommand
import os
import django
import sys
path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
if path not in sys.path:
    sys.path.append(path)
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "slp_server.settings")
django.setup()
DB_NAME = settings.DB_NAME
SEND_MAIL_TO = settings.SEND_MAIL_TO

class Command(BaseCommand):
    help = "write the text that appears when typing help command in cmd"
    
    def handle(self, *args, **kwargs):
		# write your logic here (note: you don't have to use *args or **kwargs in the actual code logic)
```