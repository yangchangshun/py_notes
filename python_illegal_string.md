# python 非法字符


> 在python中`\0`表示八进制，`\x`表示十六进制, `0b`表示二进制,十进制不解释。

最近写一个脚本，目的是从其他系统获取数据经过处理，然后写入到execl。但是其中遇到一个问题就是，数据中包含一些特殊字符，openpyxl库认为是非法字符。

```
def replace_illegality(s):
    # s = str(s).replace(u'\b', '')
    ILLEGAL_CHARACTERS_RE = re.compile(r'[\000-\010]|[\013-\014]|[\016-\037]')
    s = ILLEGAL_CHARACTERS_RE.sub(r'', str(s))
    return s

```



