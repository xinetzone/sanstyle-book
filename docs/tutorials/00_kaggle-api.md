(kaggle-api)=
# Kaggle 命令行工具

参考：[Public API Documentation | Kaggle](https://www.kaggle.com/docs/api)

kaggle 命令行工具安装：

```shell
pip install kaggle
```

- Mac/Linux 推荐安装

```
pip install --user kaggle
```

安装完成之后，在 API 栏目，点击 `Create API Token` 按钮，触发浏览器下载包含 API 凭证的 json 文件 `kaggle.json` ，并将其放在 `~/.kaggle` 文件夹下：

```json
{
 "username": "",
 "key": "",
 "path": ""
}
```

其中，`username` 字段是 kaggle 账户的用户名，`key` 字段，则是用户的专属 API Key。`path` 字段即 Kaggle 下载数据集的目录。如果不设置 `path` 字段，Kaggle 默认的下载目录是用户主目录即 `$HOME`。

## 使用 `competitions` 进行交互

Kaggle API 和 CLI 工具提供了在 Kaggle 上与 Competitions 交互的简单方法。可用的命令可以使参与竞赛成为模型构建工作流的无缝组成部分。

* `kaggle competitions list`：列出目前正在进行的比赛
* `kaggle competitions download -c [COMPETITION]`：下载与比赛相关的文件
* `kaggle competitions submit -c [COMPETITION] -f [FILE] -m [MESSAGE]`：提交参赛作品

## 使用 `datasets` 进行交互

Kaggle API 和 CLI 工具提供了与 Kaggle 上的数据集交互的简单方法。可用的命令可以使搜索和下载 Kaggle 数据集成为您的数据科学工作流的无缝部分。

* `kaggle datasets list -s [KEYWORD]`：列出匹配搜索项的数据集
* `kaggle datasets download -d [DATASET]`：下载与数据集关联的文件

## 创建新的数据集

以下是在 Kaggle 上创建新数据集的步骤：

* 创建一个包含要上传的文件的文件夹
* 运行 `kaggle datasets init -p /path/to/dataset`  输出 [metadata 文件](https://github.com/Kaggle/kaggle-api/wiki/Dataset-Metadata)
* 数据集的元数据添加到生成的 `datapackage.json` 文件中
* 运行 `kaggle datasets create -p /path/to/dataset` 创建数据集
* 运行 `kaggle datasets version -p /path/to/dataset -m "Your message here"` 创建数据集的版本

默认情况下，您的数据集是私有的。您也可以添加一个 `-u` 标志，使其公共时，您创建它，或导航到“设置”>“共享”从您的数据集的页面，使其公共或与合作者共享。

## 其他

为了方便本地电脑使用数据集，可以定义数据集根目录：

```python
def kaggle_root():
    import kaggle
    config_values = kaggle.api.config_values
    root = config_values['path']
    return root
```