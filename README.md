# jmurabe.centos7base for Scaleway
Vagrant + Ansible で [Scaleway](https://www.scaleway.com/") にCentOS7のインスタンスを起動し、CEFSプロジェクト提供のエラッタに基づきセキュリティアップデートを行います。

Scalewayのトークン(SCALEWAY_TOKEN)、組織ID(SCALEWAY_ORG)などの公開するべきではない情報は.envファイルで管理します。


## 使用 Vagrant Plugin
未導入の場合は導入してください。

```
$ vagrant plugin install vagrant-scaleway
$ vagrant plugin install dotenv
```

## 設定
```
$ git clone git@github.com:jmurabe/scaleway-centos7base.git
$ cd scaleway-centos7base
```

.env.exampleを参考に.envファイルを作成してください。

.env.example

```
TARGET = 'scaleway'
#TARGET = 'centos/7'
# for Scaleway
SCALEWAY_TOKEN = 'your Scaleway token'
SCALEWAY_ORG = 'your Scaleway organization id'
SCALEWAY_PKEY = '~/.ssh/id_rsa'

```

- TARGET
	- scalewayにするScalewayで、他だとbox名として扱いVirtualBoxで動作します。
- SCALEWAY_TOKEN
    -  Scalewayコントロールパネル、ユーザーのCredentialsで作成します。
- SCALEWAY_ORG
	- 組織ID
	- 確認方法の例: curl https://account.cloud.online.net/organizations -H "X-Auth-Token: SCALEWAY_TOKEN"
- SCALEWAY_PKEY
	- Scalewayに登録した公開鍵の秘密鍵を指定します。

## 使用方法

インスタンス起動

```
$ vagrant up
```

## 参照
- [VagrantでScaleway使うと開発に便利なのでは？という話](http://www.lancard.com/blog/2017/09/08/vagrant%E3%81%A7scaleway%E4%BD%BF%E3%81%86%E3%81%A8%E9%96%8B%E7%99%BA%E3%81%AB%E4%BE%BF%E5%88%A9%E3%81%AA%E3%81%AE%E3%81%A7%E3%81%AF%EF%BC%9F%E3%81%A8%E3%81%84%E3%81%86%E8%A9%B1/)
- [CentOS7 での yum –security update 事情](http://www.lancard.com/blog/2017/09/15/centos7-%e3%81%a7%e3%81%ae-yum-security-update-%e4%ba%8b%e6%83%85/)
