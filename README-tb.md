# LEDE 源码 + luci 仓库 同步到 GitHub 完整教程
## 一、前置准备
1. 已安装 Git（终端执行 `git --version` 可验证，无则执行 `sudo apt install git` 安装）
2. GitHub 账号（拥有 Namia-kair/lede、Namia-kair/luci 仓库的推送权限）
3. GitHub Personal Access Token (PAT)（生成时勾选 `repo` 全权限，保存好令牌）
4. 本地目录：/mnt/Teclast/lede（LEDE 主源码）、/mnt/Teclast/luci（luci 源码）

## 二、全局配置 Git 身份（仅首次执行）
```bash
# 配置 GitHub 用户名（替换为你的账号 Namia-kair）
git config --global user.name "Namia-kair"
# 配置 GitHub 绑定邮箱（替换为你的邮箱）
git config --global user.email "kmy258855@outlook.com"
# 可选：缓存凭证（避免每次推送输入账号，有效期3600秒=1小时）
git config --global credential.helper 'cache --timeout=3600'
```bash
###  三、LEDE 源码同步到 GitHub（/mnt/Teclast/lede）
步骤 1：进入 LEDE 目录
