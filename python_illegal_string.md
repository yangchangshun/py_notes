# python 非法字符


> 在python中`\0`表示八进制，`\x`表示十六进制, `0b`表示二进制,十进制不解释。

最近写一个脚本，目的是从其他系统获取数据经过处理，然后写入到excel。但是其中遇到一个问题就，数据中包含一些特殊字符，openpyxl库认为是非法字符,无法写入到excel中。python表示的特殊字符如下：
`re.compile(r'[\000-\010]|[\013-\014]|[\016-\037]')`
我的解决方案如下：

```python
def replace_illegality(s):
    # s = str(s).replace(u'\b', '')
    ILLEGAL_CHARACTERS_RE = re.compile(r'[\000-\010]|[\013-\014]|[\016-\037]')
    s = ILLEGAL_CHARACTERS_RE.sub(r'', str(s))
    return s

```
其实`\000`就是用八进制表示的而已，对应的十六进制`\x00`，对应的特殊字符`空字符`。查看ASCII表一目了然,下表是一个缩写

Bin(二进制) | Oct(八进制)	| Dec(十进制)| Hex(十六进制) |缩写/字符| 解释
|   :---:  |    :---:  |  :---:    |    :---:     | :---:  | ---|
 0000 0000| 0       |  0        |      00      | NUL(null) | 空字符
