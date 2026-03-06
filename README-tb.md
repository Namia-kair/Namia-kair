# LEDE 源码 + luci 仓库 同步到 GitHub 完整教程
## 一、前置准备
1. 已安装 Git（终端执行 `git --version` 可验证，无则执行 `sudo apt install git` 安装）
2. GitHub 账号（拥有 Namia-kair/lede、Namia-kair/luci 仓库的推送权限）
3. GitHub Personal Access Token (PAT)（生成时勾选 `repo` 全权限，保存好令牌）
4. 本地目录：/mnt/Teclast/lede（LEDE 主源码）、/mnt/Teclast/luci（luci 源码）

###   二、全局配置 Git 身份（仅首次执行）

# 配置 GitHub 用户名（替换为你的账号 Namia-kair）
git config --global user.name "Namia-kair"
# 配置 GitHub 绑定邮箱（替换为你的邮箱）
git config --global user.email "kmy258855@outlook.com"
# 可选：缓存凭证（避免每次推送输入账号，有效期3600秒=1小时）
git config --global credential.helper 'cache --timeout=3600'

# 三、LEDE 源码同步到 GitHub（/mnt/Teclast/lede）
步骤 1：进入 LEDE 目录

运行
cd /mnt/Teclast/lede
# 步骤 2：查看本地修改（可选，确认要同步的内容）
bash
运行
git status
# 步骤 3：暂存所有本地修改
bash
运行
# 暂存所有新增/修改/删除的文件
git add .
# 若仅同步指定文件，示例：git add feeds.conf.default package/base-files/files/etc/banner
步骤 4：提交修改（必须写清晰的提交说明）
bash
运行
git commit -m "LEDE：调整banner文件、修改config_generate、更新feeds配置"
# 提交说明可根据实际修改调整，比如：LEDE：新增qmodem插件、修复编译警告
步骤 5：推送到 GitHub 远程仓库
bash
运行
# 推送本地master分支到远程origin/master（若默认分支是main，替换为main）
git push origin master
推送时认证：
用户名：输入 Namia-kair
密码：输入 GitHub 生成的 PAT（ghp_开头的令牌，非登录密码）
# 步骤 6：解决常见问题
网络解析失败（Could not resolve host: github.com）：
bash
运行
# 配置 Git 代理（替换为你的代理端口，如 Clash 的 7890）
git config --global https.proxy http://127.0.0.1:7890
# 推送完成后可取消代理（可选）
# git config --global --unset https.proxy
本地修改与远程冲突：
bash
运行
# 暂存本地修改 → 拉取远程最新 → 恢复本地修改 → 解决冲突
git stash push -m "backup_lede_mod"
git pull origin master
git stash pop
# 解决冲突后重新提交：git add . && git commit -m "解决冲突，合并远程代码"
四、luci 仓库同步到 GitHub（/mnt/Teclast/luci）
步骤 1：进入 luci 目录
bash
运行
cd /mnt/Teclast/luci
步骤 2：查看本地修改（可选）
bash
运行
git status
步骤 3：暂存所有本地修改
bash
运行
git add .
# 若仅同步指定插件，示例：git add applications/luci-app-xupnpd/
# 步骤 4：提交修改
bash
运行
git commit -m "luci：新增xlnetacc/xupnpd/zerotier插件，调整zerotier文件权限"
# 提交说明根据实际修改调整，比如：luci：优化zerotier界面、新增中文翻译
# 步骤 5：推送到 GitHub 远程仓库
bash
运行
git push origin master
认证方式：与 LEDE 推送一致（用户名 Namia-kair + PAT）
# 五、验证同步成功
终端验证：推送完成后无 error/fatal 提示，显示 master -> master 即成功；
网页验证：打开 GitHub 仓库页面（https://github.com/Namia-kair/lede 、https://github.com/Namia-kair/luci），刷新后能看到最新提交记录和修改的文件。
# 六、后续同步简化流程（修改代码后重复执行）
bash
运行
# 以 LEDE 为例，luci 操作完全一致
cd /mnt/Teclast/lede
git add .
git commit -m "本次修改说明"
git push origin master
七、关键注意事项
PAT 是核心凭证，切勿泄露，丢失后需在 GitHub 重新生成；
推送前建议先执行 git pull origin master，避免本地与远程代码冲突；
提交说明要清晰，方便后续追溯修改内容；
若仓库默认分支是 main（GitHub 新仓库默认），需将所有命令中的 master 替换为 main。
plaintext

### 使用说明
1. 直接复制上述全部内容，粘贴到文本编辑器后保存为 `README.md`；
2. 可直接放到 `/mnt/Teclast/` 目录下，或上传到 GitHub 仓库根目录；
3. 所有命令保持原样本的完整性，markdown 格式下代码块高亮显示，层级清晰易读。
