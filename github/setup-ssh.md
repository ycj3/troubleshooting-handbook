# GitHub SSH 密钥配置指南（macOS）

本文档介绍如何在 macOS 上生成并配置 SSH 密钥，以便通过 SSH 安全地连接到 GitHub。

## 1. 检查是否已有 SSH 密钥

打开终端，输入以下命令：

```bash
ls -al ~/.ssh
```

如果能看到以下文件之一：

```
id_rsa.pub
id_ed25519.pub
```

说明你的系统中已经存在 SSH 密钥。

如果没有，请继续下一步生成新的密钥。

## 2. 生成新的 SSH 密钥

我们将在 `~/.ssh` 目录下生成一个名为 `github_id_ed25519` 的新密钥：

```bash
ssh-keygen -t ed25519 -C "你的GitHub邮箱" -f ~/.ssh/github_id_ed25519
```

**参数说明：**

- `-t ed25519`：指定使用 Ed25519 算法（推荐）
- `-C`：添加注释，通常填写你的 GitHub 邮箱
- `-f`：指定密钥文件名和保存路径

生成过程中会提示输入密码短语（passphrase）：

- 可直接按回车跳过；
- 或输入一个密码以提高安全性。

生成完成后，将得到两个文件：

```
~/.ssh/github_id_ed25519        # 私钥（请妥善保管，不可泄露）
~/.ssh/github_id_ed25519.pub    # 公钥（可安全上传至 GitHub）
```

## 3. 将密钥添加到 SSH Agent

启动 SSH agent 并添加新密钥：

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_id_ed25519
```

## 4. 将公钥添加到 GitHub 账户

查看并复制公钥内容：

```bash
cat ~/.ssh/github_id_ed25519.pub
```

然后前往 GitHub 设置页面：
👉 [https://github.com/settings/keys](https://github.com/settings/keys)

点击 **“New SSH key”** → 粘贴公钥内容 → 点击 **“Add SSH key”** 保存。

## 5. 配置 SSH 使用该密钥

创建或编辑 SSH 配置文件：

```bash
nano ~/.ssh/config
```

添加以下内容：

```bash
Host github.com
  HostName ssh.github.com
  User git
  Port 443
  IdentityFile ~/.ssh/github_id_ed25519
  IdentitiesOnly yes
```

保存并退出：

- 按 `Ctrl + O` → 回车保存；
- 按 `Ctrl + X` 退出编辑。

## 6. 测试 SSH 连接是否成功

执行：

```bash
ssh -T git@github.com
```

如果显示：

```
Hi <你的GitHub用户名>! You've successfully authenticated, but GitHub does not provide shell access.
```

🎉 恭喜！SSH 密钥已成功配置！

## 7. 使用 SSH 克隆仓库

现在可以通过 SSH 克隆你的 GitHub 仓库了
