```py
# -*- coding: utf-8 -*-

from fabric.api import *

env.gateway = 'root@0.0.0.0:22'
env.passwords = {
    'root@0.0.0.0:22': '123456'
}

env.roledefs.update({
    'mysql': ['192.168.1.2'],
    'redis': ['192.168.1.3', '192.168.1.3']
})

env.user = 'wujie'
env.password = '123456'

@task
@roles('mysql', 'redis')
def xxx():
    run("set name = `jps -lv | grep java | awk '{print $1}'`; echo $name", shell=False)


if __name__ == '__main__':
    execute(xxx)

```
