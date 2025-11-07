# Git Pull/Push

cd /d/Code/0_Work/Intern/Baiology/WixAdminAPI/

git status

git pull origin main

git add .

git commit -m "Message"

git push origin main



git diff

git diff -cache

| 操作      | 说明                    |
| --------- | ----------------------- |
| `q`       | 退出                    |
| `↑ ↓`     | 上下滚动                |
| `space`   | 向下翻页                |
| `b`       | 向上翻页                |
| `/关键字` | 搜索内容                |
| `n` / `N` | 下一个 / 上一个搜索结果 |



Seeing difference between remote and local

git fetch origin
git diff origin/main -- BaiologyWixAdminAPI/Controllers/UserWeeklyGoalController.cs