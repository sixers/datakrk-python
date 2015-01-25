DataKRK #9 - Python for Data Science
------------------------------------

This repository contains notebooks & data from my talk at [DataKRK](http://www.meetup.com/datakrk/events/219351697/)

Online versions:

- **Python for Data Science**  
  http://nbviewer.ipython.org/gist/sixers/76e9786d9bb46af59d61
- **PySpark**  
  http://nbviewer.ipython.org/gist/sixers/ed53012eee63582a80a3
  
  
# Requirements

- `ipython`
- `numpy`
- `scipy`
- `pandas`
- `scikit-learn`
- `matplotlib`
- `ggplot`

I recommend using [Anaconda](https://store.continuum.io/cshop/anaconda/), and installing ggplot from [head](https://github.com/yhat/ggplot)

# PySpark

In order to run PySpark code, you need to setup a Spark cluster (AWS EMR has built-in support for Spark), but probably you can also run it on your local machine in standalone mode.

Install IPython and create new profile for PySpark:

```bash
$ ipython profile create pyspark
```

Edit `~/.ipython/profile_pyspark/ipython_config.py` and paste:
```
c = get_config()

c.NoteBookApp.ip = '*'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8743 # or whatever you want; be aware of conflicts with CDH
```
Edit ` ~/.ipython/profile_pyspark/startup/00-pyspark-setup.py` and paste:
```
import os
import sys
 
ENVS = {
    'PYSPARK_PYTHON': 'python2.7',
    "MASTER": "yarn-client",
    "SPARK_HOME": '/home/hadoop/spark/',
    'PYSPARK_SUBMIT_ARGS': '--jars /home/hadoop/spark/lib/spark-examples-1.1.0-hadoop2.4.0.jar',
}

def set_envs():
    for key, val in ENVS.iteritems():
        os.environ[key] = val


set_envs()
SPARK_HOME = os.environ['SPARK_HOME']
sys.path.insert(0, os.path.join(SPARK_HOME, 'python'))
sys.path.insert(0, os.path.join(SPARK_HOME, 'python/lib/py4j-0.8.2.1-src.zip'))
execfile(os.path.join(SPARK_HOME, 'python/pyspark/shell.py'))
```


Run `ipython notebook --profile=pyspark`



