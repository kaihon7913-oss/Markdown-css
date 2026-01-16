# SSH 帳號設定
- https://blog.csdn.net/weixin_42310154/article/details/118340458

---

# GitHub 部署
1️⃣ 安裝 Git（如果還沒安裝）

在終端機（Terminal / Git Bash / PowerShell）輸入：

git --version


如果看到版本號，代表已安裝。

如果沒安裝，請到 Git 官方網站
 下載安裝。

2️⃣ 生成 SSH Key（如果還沒設定過）

在終端機輸入：
```cmd
ssh-keygen -t ed25519 -C "你的_email@example.com"
```

按 Enter 接受預設儲存位置（通常是 ~/.ssh/id_ed25519）

可以設密碼（或直接 Enter 不設）

接著啟用 SSH Agent 並加入金鑰：

# 啟動 SSH agent
```cmd
eval "$(ssh-agent -s)"
```
# 加入金鑰
```cmd
ssh-add ~/.ssh/id_ed25519
```
3️⃣ 將 SSH Key 加入 GitHub

打開 GitHub → 點右上角你的頭像 → Settings → SSH and GPG keys → New SSH key

複製公鑰（id_ed25519.pub）內容：
```cmd
cat ~/.ssh/id_ed25519.pub
```

貼上到 GitHub 的 Key 欄位，給個名稱（例如「My Laptop」），按 Add SSH key。

測試連線：
```cmd
ssh -T git@github.com
```

如果成功，會顯示：

Hi username! You've successfully authenticated, but GitHub does not provide shell access.

4️⃣ 在 GitHub 建立一個新的 Repository

點右上角 + → New repository

Repository 名稱（例如 my-project）

選擇公開或私人

不要勾選「Initialize this repository with a README」(我們會從本地上傳)

建立 Repository

此時 GitHub 會給你 SSH 的 URL，例如：

git@github.com:你的帳號/my-project.git

5️⃣ 本地專案設定 Git

假設你的專案在某個資料夾，例如 ~/projects/my-project：

cd ~/projects/my-project


初始化 Git：
```cmd
git init
```

設定使用者名稱與 Email：

git config --global user.name "你的名字"
git config --global user.email "你的_email@example.com"

6️⃣ 新增檔案並提交 (commit)

新增檔案：
```cmd
git add .
```

提交：

git commit -m "Initial commit"

7️⃣ 連結 GitHub Repository（SSH）
git remote add origin git@github.com:你的帳號/my-project.git


檢查是否成功：
```cmd
git remote -v
```

會看到：
```cmd
origin  git@github.com:你的帳號/my-project.git (fetch)
origin  git@github.com:你的帳號/my-project.git (push)
```
8️⃣ 推送到 GitHub
```cmd
git branch -M main   # 將分支改為 main (如果尚未建立)
git push -u origin main
```

第一次推送可能會要求你確認 SSH 連線，輸入 yes 即可。
之後就可以用：
```cmd
git push
```

來更新。

✅ 完成！

這樣就完成 從零開始用 SSH 上傳專案到 GitHub 的流程了。
以後修改後只需要：

```cmd
git add .
git commit -m "修改說明"
git push
```

最後請用jsdelivr轉檔才能使用
- https://www.jsdelivr.com/github


你想要我幫你做嗎？
