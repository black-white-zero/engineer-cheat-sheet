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
    xxx()
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

### 时间
时间戳转为当地时间字符串
```python
string_time = time.strftime("%Y-%m-%d %H:%M", time.localtime(timestamp))
```

时间戳转为 UTC 时间字符串
```python
utc_time = datetime.utcfromtimestamp(transaction["blockTime"])
utc_string_time = utc_time.strftime("%Y-%m-%d %H:%M:%S")
```

当地时间字符串转为时间戳
```python
import time
from datetime import datetime

str_time = "2020-06-02 04:58:49"
struct_time = datetime.strptime(str_time, "%Y-%m-%d %H:%M:%S")
timestamp = struct_time.timestamp()

print(timestamp)
```

UTC 字符串转为时间戳
```python
import time
from datetime import datetime, timezone

str_time = "2020-06-02 04:58:49"
struct_time = datetime.strptime(str_time, "%Y-%m-%d %H:%M:%S")
utc_struct_time = struct_time.replace(tzinfo=timezone.utc)
timestamp = utc_struct_time.timestamp()

print(timestamp)
```

### 正则表达式
构造新的正则表达式进行正则表达式匹配。
```python
import re

evidence_exchange_list = ["huobi", "binance"]
pattern = '|'.join(evidence_exchange_list)

if re.search(pattern, "Huobi”, re.I) != None:
    pass
```

### 导入

```python
import sys
sys.path.append('../')
```

## 业务

### BTC 交易数据解析 USDT 交易

BTC 原数据解析 USDT 转入转出地址和转移值。
```python
# 判断是否为 USDT-Omni 交易
is_usdt_omni = False
vouts = transaction["vout"]
usdt_op_return = ""
for vout in vouts:
    address = vout["addresses"][0]
    if "#31" in address:
        is_usdt_omni = True
        usdt_op_return = address
        break

# 解析 USDT-Omni 的输入输出地址 sender recipient
vins = transaction["vin"]
vouts = transaction["vout"][::-1]
sender = vins[0]["addresses"][0]

had_changed = False
recipient = vouts[0]
for vout in vouts:
    is_address = vout["isAddress"]

    if is_address:
        maybe_output_address = vout['addresses'][0]
        if had_changed:
            recipient = maybe_output_address
            break

        if maybe_output_address != sender:
            recipient = maybe_output_address
            break
        else:
            had_changed = True

# 获取 value 值 amount
usdt_op_return_list = usdt_op_return.split(" ")
amount = round(float(usdt_op_return_list[3]), 3)

# 排除 sender recipient 都不是查询地址的情况
if (sender == address) or (recipient == address):
    pass
```

### 不同币种正则
```python
pattern_eth = r'^0x[a-fA-F0-9]{40}$'
regex_eth = re.compile(pattern_eth)


_pattern = r'^(([13][a-km-zA-HJ-NP-Z0-9]{26,33},*)|(bc(0([ac-hj-np-z02-9]{39}|[ac-hj-np-z02-9]{59})|1[ac-hj-np-z02-9]{8,87}),*))+$'
regex_btc = re.compile(pattern_btc)

pattern_xrp = r'^r[0-9a-zA-Z]{24,34}$'
regex_xrp = re.compile(pattern_xrp)

pattern_trx = r'^T[0-9a-zA-Z]{33}$'
regex_trx = re.compile(pattern_trx)

pattern_eos = r'^[a-z1-5][a-z1-5\.]{0,10}[a-z1-5]?$'
regex_eos = re.compile(pattern_eos)
```

## 日志

### 装饰器 - 函数运行显示运行日志

```python
import functools

from loguru import logger

def func_run_log(func):
    """函数运行显示运行日志"""

    @functools.wraps(func)
    def wrapper(*args, **kw):
        logger.info('调用函数: %s, 参数: %s' % (func.__name__,
                                          kw))
        return func(*args, **kw)
    return wrapper
```

### 装饰器 - 函数报错显示错误跟踪

```python
import functools
import traceback

from loguru import logger

def validate(f):
    @functools.wraps(f)
    def decorator(*args,**kw):
        try:
            data = f(*args,**kw)
        except Exception as e:
            logger.error('发生错误：{}',traceback.format_exc())
            data = None
        return data
    return decorator
```