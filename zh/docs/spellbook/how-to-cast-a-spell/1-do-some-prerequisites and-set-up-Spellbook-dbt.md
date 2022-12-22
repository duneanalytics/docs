---
title: 1. 💻 准备一些先决条件并且设置好魔法书 dbt
description: 以下是设置计算机以在魔法书上工作所需执行的操作。
---

你需要安装下述软件来开始：

* [VSCode](https://code.visualstudio.com/)（任何IDE都可以，但我们使用的是这个）
* [Python 3.9](https://realpython.com/installing-python/)（您需要安装这个确切版本的 Python 和 distutils； 如果您遇到问题，请在我们的[#spellbook Discord channel!](https://discord.com/channels/757637422384283659/999683200563564655)提问）
* [pip](https://pip.pypa.io/en/stable/installation/)
* [pipenv](https://pypi.org/project/pipenv/)
* [git and GitHub](https://docs.github.com/en/get-started/quickstart/set-up-git) (包括认证)

安装了上述软件之后，你还需要：

* 为[魔法书仓库](https://github.com/duneanalytics/spellbook)这个库做一个[分叉（Fork）](https://docs.github.com/en/get-started/quickstart/fork-a-repo)。包括克隆到本地和添加上游库链接。
* 查看Gitbut上关于如何从分叉中发出合并请求的[说明](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)。

这是一个展示如何创建 Spellbook 存储库的分支的快速视频：

![type:video](https://drive.google.com/file/d/1wGGhgwUsersdvqq4YpDWRMRSgqd8l8Qd/preview)

本质上，你需要：

1. 转到 Spellbook 存储库并单击顶部的 fork 按钮。
2. 复制你的 fork 的存储库的 HTTPS URL
3. 打开你想要在 VS Code 中存储 Spellbook 的文件夹
4. 在 VS code 中打开终端并输入 `git clone [paste your URL here]`

按下回车键后就会开始下载 Spellbook，这将需要几分钟时间。

## 配置 Spellbook dbt

有了 Spellbook 分支的本地副本后，就可以设置 Spellbook dbt 了！

如果尚未安装，请在 VSCode 中打开 Spellbook 分支的本地副本，然后打开终端并输入 `pipenv install`。

这将安装在您的计算机上运行 Spellbook 所需的软件包。

安装完成后，运行 `pipenv shell` 以激活您的虚拟环境。

然后运行 `dbt init` 来初始化dbt。

在随后的每个提示中输入这些值：

```

1. Enter a number: 2 [choose databricks]
2. host (yourorg.databricks.com): . [enter “.”]
3. http_path (HTTP Path): .
4. token (dapiXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX): [just hit enter at first]
    1. [1] use Unity Catalog
    2. [2] not use Unity Catalog
5. Desired unity catalog option (enter a number): 2
6. schema (default schema that dbt will build objects in): wizard
7. threads (1 or more) [1]: 2

```

不要运行 `dbt debug`，因为您没有（或不需要）所需的凭据，运行将会失败。

保存此配置后，运行 `dbt deps` 以安装依赖项。

这个过程大致是这样的：

![type:video](https://drive.google.com/file/d/1V0SARSZ4RmjuroX0ysmFgDf7w7ImaYBT/preview)

最后，运行 `dbt compile`.

如果运行正确，您的终端应该以“done”结束，您应该在侧边栏中看到”target“文件夹。

![target folder success](images/target-folder-success.jpg)

然后，运行 `git checkout -b workshop` 创建一个名为“workshop”的新本地存储分支，用于执行本指南中的练习工作。

最后，运行 `git push -u origin workshop` 将您的本地“workshop”分支添加或“推送”到您的远程 GitHub 存储库，以便我们最终可以发出我们的魔法书合并请求。