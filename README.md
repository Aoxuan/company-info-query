# Company Info Query

企查查企业信息与风险调查技能。用于签约前查询企业主体信息、三要素一致性及经营/司法风险，并按 `legal-draft-2026-08-13` 规则输出低、中、高风险等级。

本仓库是可直接放入 zcode、Cursor 或 Hermes `skills` 目录的自包含技能包。技能入口与使用流程见 [SKILL.md](SKILL.md)。

## 功能

- `check`：检查企查查凭据和远程 MySQL 连通性
- `search`：模糊搜索企业候选（约 0.10 元/次）
- `profile`：查询企业详情和风险，保存快照、写入 MySQL 并生成 Excel（约 7.50 元/次）
- `export`：从已有快照离线重生成 Excel，不调用企查查

## 安装

运行环境要求 Windows 64 位、Python 3.11。没有 Python 时，按 [INSTALL.md](INSTALL.md) 安装。

把仓库克隆到宿主平台的 `skills` 目录：

```powershell
git clone https://github.com/Aoxuan/company-info-query.git
cd company-info-query
py -m pip install -r requirements.txt
```

复制配置模板并填写：

```powershell
Copy-Item .env.example .env
```

以下环境变量均为必填：

- `QCC_APP_KEY`
- `QCC_SECRET_KEY`
- `MYSQL_HOST`
- `MYSQL_PORT`
- `MYSQL_USER`
- `MYSQL_PASSWORD`
- `MYSQL_DB`

配置后自检：

```powershell
py scripts/query.py check
```

`check` 通过后，平台智能体可按 [SKILL.md](SKILL.md) 编排 `search → profile` 两阶段查询。宿主平台须允许技能执行本机终端命令；若 Hermes 使用隔离运行时，应在该运行时提供 Python 3.11 和上述环境变量。

## 数据与安全

- `.env`、真实密钥、企业快照、Excel、审计日志不进入仓库
- 企查查数据仅用于内部风控审批，不得二次分发
- `profile` 会产生企查查费用，非必要不要重复查询
- 本技能只读查询并提示风险，不自动决定拦截、放行或签约

## 目录

```text
company-info-query/
├── SKILL.md
├── INSTALL.md
├── manifest.yaml
├── requirements.txt
├── .env.example
├── scripts/
│   ├── query.py
│   ├── common/
│   └── qcc/
└── references/
```

