# bdsf
Bear's distributed spider framework

- Prerequisite
  - Python 2.X or 3.X are both OK.
  - MySQL
  - Redis
  - Python libs: peewee, redis, requests, selenium (Chrome driver recommended)
  - Use redis-cli ping to check if redis started, if OK it will receive 'PONG'.
  
- Schduler (ds_scheduler.py): Used to schedule the task and put the jobs to queue.
  - Argument '-c', '--config':
    - Assign config file to use, refer ds_config.py as template.
  - Argument '-a', '--action':
    - create: create a new task
    - view: view and update task status, need provide task_id.
    - retry: retry unfinished jobs in the task, need provide task_id.
  - Argument '-t', '--task_id':
    - Assign task_id for view/retry action.
  - Usage sample:
    - python ds_scheduler.py -c ds_config -a create
    - python ds_scheduler.py -a view -t 1
    - python ds_scheduler.py -a retry -t 1
    
- Worker (ds_worker.py): Used to get job from queue, run it, write back result and job status back to database.
  - Argument '-c', '--config':
    - Assign config file to use, refer ds_config.py as template.
  - Argument '-s', '--spider':
    - Assign the spider implementation used, refer spider_sample.py as reference, 'parse' is the required interface to implement.
  - Argument '-t', '--thread_count':
    - Assign how many threads used. 0 is default, means the thread count equals the CPU core count.
  - Usage:
    - python ds_worker.py -c ds_config -s spider_sample -t 2
    
- Data preparation:
  - Open ds_config.py, edit 'DB' to your local settings.
  - Run 'python ds_database.py' to create the tales, ds_config.py is used by default.
  - data.sql contains the sample data, you can fill it in the database for some experiment.
  
Wish you like it!  
QQ: 859189803

51CTO小广告：
- 面向测试工程师的Python学习：http://edu.51cto.com/course/8711.html
- 性能测试面必知必会系列：http://edu.51cto.com/course/10180.html
