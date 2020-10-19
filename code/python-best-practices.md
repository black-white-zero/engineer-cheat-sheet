


## 单元测试
单元测试保证后续对代码的更改不会引入新的 Bug。

```python
import unittest

class Testxxx(unittest.TestCase):
    
    def test_xxx(self):

        self.assertEqual(xxx, True)
        pass
```