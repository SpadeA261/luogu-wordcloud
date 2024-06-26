# luogu-wordcloud

![](https://github.com/konyakest/luogu-wordcloud/blob/main/image.png)

从 luogu 提交记录爬取代码，并生成词云

## 安装

```bash
git clone https://github.com/konyakest/luogu-wordcloud.git
cd luogu-wordcloud/
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 使用

首先，需要填写 ``configs.json``

最简单的 ``configs.json`` 如下：

```json
{
    "spider_configs": {
        "uid": 482660,
        "client_id": "xxxxxxxxxxxxxxx"
    }
}
```

然后运行 ``python3 spider.py`` 和 ``python3 cloud.py`` 即可生成词云

## 选项

提供了以下额外选项：

``spider_configs`` 中：

- ``difficulties``：选择的题目的难度范围，例如 "``012``" 表示选择“灰，红，橙”，默认为“``567``”（“蓝，紫，黑”）
- ``person_uid``：指定要爬取的用户的用户名，默认为 ``uid`` 的值
- ``save_files``：是否保存爬取到的代码，默认为 ``false``
- ``files_dir_name``：将代码保存在哪个文件夹下，默认为 ``codes``
- ``sample_count``：从题目中随机选择若干道题进行爬取，不填表示选择全部

``cloud_configs`` 中：

- ``output_size``：输出的图片的长宽，默认为 1000
- ``output_file``：输出的图片文件名，默认为 ``wordcloud.png``
- ``background_color``：背景颜色，默认为 ``white``
- ``ignore_words``：去掉这些关键词
- ``ignore_cnt``：去掉出现次数多于此值的关键词，默认为 10000
- ``filter``：按照一个 ``lambda`` 过滤关键词，默认为 ``lambda x:True``，该 ``lambda`` 传入一个长度为 2 的 ``list``（``[word, cnt]``），返回 ``bool``

    例如 ``lambda x:len(x[0]) >= 2 and x[1]<=1000`` 选择所有长度大于等于 2 且出现次数小于等于 1000 的单词

具体用法可参见 ``all_configs.json``
- ``mask``：指定遮罩图片
- ``scale``：指定相对于遮罩图片的放大倍数，默认为 1（指定了遮罩图片后，``output_size`` 项失效）