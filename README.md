# NeteaseMusicApi
一个网易云音乐的Api

## ~~食用~~使用教程
1. 使用pip安装 `pip install nemusicapi`
2. 导入包，创建api
   ```python
   import nemusicapi
   api = Api()
   ```
3. 然后就可以愉快的使用了

## 举个~~栗子~~例子
```python
import os
from NEmusicApi import Api, QualityLevel

download_dir = './download'
cookie = '这里输入cookie'

api = Api(cookie=cookie, download_dir=download_dir)


def main(raw_song_name: str):
    res = api.get_song_data(raw_song_name, limit=1)
    if res is None:
        return
    song_id = list(res.keys())[0]
    song_name = list(res.values())[0]
    
    level = QualityLevel.hires
    res = api.get_song_download_data(song_id, level=level)
    if res is None:
        return
    song_url, song_type = res
    
    file_name = f'{song_name}_{level.value}.{song_type.value}'
    if not os.path.exists(os.path.join(download_dir, file_name)):
        api.download_song(song_url, file_name)


if __name__ == '__main__':
    main('这里输入歌曲名')
```

## 注意事项
* 创建api的时候，不输入`cookie`或者cookie对应的账号没有vip，都有可能导致获取信息不完整，需要自己测试
* 创建api的时候，不输入`download_dir`，在使用`download_song`方法的时候会raise异常

## 单元测试
1. `poetry run python .\test\test_api.py`
2. `poetry run python .\test\test_base_api.py`