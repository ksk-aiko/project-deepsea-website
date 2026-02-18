# EC2からGitHubのprivateリポジトリを安全にcloneする：Machine User + SSH鍵の完全ガイド

## リード文

EC2や本番サーバからGitHubのprivateリポジトリをcloneしたいとき、  
「Deploy Key」「Personal Access Token」「Machine User」など複数の方法があり、どれを使うべきか迷うことがあります。

本記事では、本番環境で最もスケーラブルで安全な方法である

> **Machine User + SSH鍵方式**

を使って、

- EC2からprivateリポジトリをcloneする方法
- 複数リポジトリを安全に管理する方法
- 本番運用で推奨される構成

を、仕組みから理解できるように解説します。

---

## 前提知識

以下の基本操作ができること：

- EC2へSSH接続できる
- GitHubアカウントを持っている
- Gitの基本操作（clone, push）が分かる

---

# 本文

---

## Context（背景・問題意識）

EC2からGitHubのprivateリポジトリをcloneしようとすると：

```bash
git clone git@github.com:user/private-repo.git
