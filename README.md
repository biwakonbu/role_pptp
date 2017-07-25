# role_pptp
pptpd (vpn) サーバセットアップ用 ansible ファイル。

## 対象

- CentOS 7.2 (Sakura の VPS) 対象

## 最初にやっておく事

1. SSH の鍵の設定 (パスワードログインをオフにするかは任意で)
2. `mv ansible.cfg.sample ansible.cfg` を実行し、private_key_file に、リモートホストに設定した鍵の PATH を設定する
3. ansible.cfg ファイルの remote_user の設定を鍵を設定したユーザ名に変更する
4. `mv hosts.sample hosts` を実行し、[default] の設定を対象のホストに変更する
5. `ansible all -m ping` で疎通確認

5 が成功したら OK

## pptpd セットアップ

1. `mv roles/pptp/files/chap-secrets.sample roles/pptp/files/chap-secrets` を実行
2. roles/pptp/files/chap-secrets を設定する (初期はサンプルユーザ, サンプルパスワードになっている)
3. `ansible-playbook -i hosts main.yml` を実行
4. 対象のサーバとユーザ名, パスワードを PPTP (VPN) クライアントに設定し、接続する

問題が発生しなければ、ネットワークの経路が PPTP サーバ経由になる。  
PPTP サーバに接続が出来るが、外に転送されない場合は firewall の設定がおかしい (外部への転送の設定)。

PPTP サーバに接続が出来ない場合は、ユーザ名、パスワード、接続先情報等の設定が間違っているか、  
設定ファイル (roles/pptp/files/ 以下) の設定が状況に合っていない為、適宜修正する。
