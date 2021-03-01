# 自動草はやしLINEボット
LINEでのメッセージをトリガーにGitHubの草はやしを自動化するボットを開発しました。

## 構成

## 作業開始時
ワークフロー実行時、ログが増えてコンフリクトが起こる可能性があるので、以下を実行するようにする。
```
git pull origin master
```

## GitHub Action APIを叩く
### GET
```
curl -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/{username}/{repo}/actions/workflows
```
- username: GitHubのユーザ名
- repo: リポジトリの名前

### POST
```
curl \
  -X POST \
  -H "Authorization: token $GITHUB_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/{username}/{repo}/actions/workflows/{workflow id}/dispatches \
  -d '{"ref":"{ref}"}'
```
- $GITHUB_TOKEN: IDEか何かで取得している場合は、このままでOK。取得していない場合は、公式ページで取得する必要あり。
- username: GitHubのユーザ名
- repo: リポジトリの名前
- workflow id: ワークフローのID
  - cron: 6222966
  - push: 6222967
  - webhook: 6222968
- ref: ブランチ名