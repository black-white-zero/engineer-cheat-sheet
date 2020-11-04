## 脚本运行
防止定时任务脚本运行影响。
> TODO: 需要进行整理
```python
def exec_cmd(cmd):
    """执行指令的函数
    :param cmd: 指令
    :return:
    """
    res = os.popen(cmd)
    res_text = res.read()
    res.close()

    return res_text

filename = os.path.basename(__file__)
ps_cmd = "ps -ef|grep " + filename + "|grep -v grep| wc -l"
cmd_res = exec_cmd(ps_cmd)
running_len = int(cmd_res.split('\n')[0].strip())

if running_len > 2:
    log.info('%s is running' % filename)
else:
    usdt_erc20_transfer_out_monitor()
```

## 单元测试
单元测试保证后续对代码的更改不会引入新的 Bug。

```python
import unittest

class Testxxx(unittest.TestCase):
    
    def test_xxx(self):

        self.assertEqual(xxx, True)
        pass
```

## 数据库交互
> TODO: 需要进行整理

### ORM(对象-关系映射)

```python
from peewee import *

# 连接数据库
MYSQL_DB = MySQLDatabase(host=conf.MYSQL_IP, 
                        port=conf.MYSQL_PORT,
                        user=conf.MYSQL_USERNAME,
                        passwd=conf.MYSQL_PASSWD,
                        database=conf.MYSQL_DB)

class BaseModel(Model):
    """基础模型类"""

    class Meta:
        database = MYSQL_DB


class xxxRecord(BaseModel):
    """xxxRecord 模型类"""
    pass

    class Meta:
        db_table = 'xxx_record'
        constraints = [SQL('UNIQUE KEY(coin, address)')]

# 查询数据
xxx_datas = xxxRecord.get(watch_id=watch_id)
xxx_address = xxx_datas.address
```

## 文件打开
```python

with open(FILE_PATH + FILE_NAME, 'r') as xxx_file:
    for xxx_file_line in xxx_file.readlines():
        pass
```

## 常见代码

### 两数组取交集
```python
def get_intersection(list1, list2):
    return [x for x in list1 if x in list2]

get_intersection(["1", "2", "3", "5"], ["2", "4", "5"])
```

### 生成 hash
```python
# 生成 xxx_hash_id
raw_string = 字段1 + 字段2 + str(int(time.time()))
bytes_string = bytes(raw_string, encoding="utf8")
xxx_hash_id = hashlib.md5(bytes_string).hexdigest()
```