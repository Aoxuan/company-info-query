# 运行环境安装（需求方）

本技能用本机 `py` 跑 `scripts/query.py`。请先安装 **Python 3.11**（64 位，官方安装包），再装技能依赖。

我方提供官方安装包（例如 `python-3.11.x-amd64.exe`），请保存到本机后按下面任选一条安装。不要用 Microsoft Store 里随便一个 Python，也不要让智能体开浏览器自行下载。

装完后**新开**一个终端再验收。

## 先探测

```
py --version
```

输出含 `3.11` 即可跳到「安装技能依赖」。没有 `py` 或版本不对，走下面路 A 或路 B。

## 路 A：自行安装（点鼠标）

1. 双击我方提供的 `python-3.11.x-amd64.exe`
2. 勾选 **Add python.exe to PATH**
3. 选当前用户安装（一般不必管理员）
4. 关掉已打开的终端，新开一个，执行 `py --version`，应看到 3.11

## 路 B：静默命令（IT / PowerShell）

在安装包所在目录执行（把文件名换成实际文件名）：

```
.\python-3.11.x-amd64.exe /quiet InstallAllUsers=0 PrependPath=1 Include_pip=1
```

装完同样新开终端跑 `py --version`。被权限或安全软件拦截时改走路 A，或由管理员把 `InstallAllUsers=0` 改成 `1`。

## 安装技能依赖

在技能根目录（有 `requirements.txt` 的目录）执行：

```
py -m pip install -r requirements.txt
```

然后自检：

```
py scripts/query.py check
```

`check` 通过（企查查凭据 + MySQL 均就绪）后再做查询。凭据见同目录 `.env.example`。
