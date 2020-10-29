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


class MinePoolAddressRecord(BaseModel):
    """MinePoolAddressRecord 模型类"""
    coin = CharField(max_length=10)
    address = CharField(max_length=100)
    name = CharField(max_length=50, default="unknown")
    decode_coinbase = TextField(null=True)
    repeat = IntegerField(default=1)

    class Meta:
        db_table = 'mine_pool_address_record'
        constraints = [SQL('UNIQUE KEY(coin, address)')]

# 查询数据
address_watch_datas = AddressWatchRecord.get(watch_id=watch_id)
watch_address = address_watch_datas.address
```

## 文件打开
```python

with open(FILE_PATH + FILE_NAME, 'r') as xxx_file:
    for xxx_file_line in xxx_file.readlines():
        pass
```