# free5GC Compose — Telco DevAgent Workshop

5G コア（free5GC）の設定ファイルと IaC テンプレートを管理するリポジトリ。
AI エージェントがこのリポジトリのコードを分析・変更し、GitHub Actions で EC2 にデプロイします。

## 構成

```
├── config/                  # NF 設定ファイル
│   ├── amfcfg.yaml
│   ├── smfcfg.yaml
│   ├── upfcfg.yaml
│   └── nssfcfg.yaml
├── infra/
│   └── cloudformation.yaml  # EC2 IaC テンプレート
├── docker-compose.yaml      # free5GC Docker Compose（デプロイ後に EC2 上で使用）
└── .github/workflows/
    └── deploy.yaml          # CI/CD ワークフロー
```

## CI/CD フロー

1. `config/` 配下のファイルを変更して `main` ブランチに push
2. GitHub Actions が自動起動
3. CloudFormation で EC2 を作成（初回のみ）
4. SSH で EC2 に接続し、docker compose up で free5GC をデプロイ
