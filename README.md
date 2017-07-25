# role_pptp
pptpd (vpn) サーバセットアップ用 ansible ファイル。

## 対象

- CentOS 6.8 (Sakura の VPS) 対象

## 最初にやっておく事

1. SSH の鍵の設定 (パスワードログインをオフにするかは任意で)
2. `mv ansible.cfg.sample ansible.cfg` を実行し、private_key_file に、リモートホストに設定した鍵の PATH を設定する
3. ansible.cfg ファイルの remote_user の設定を鍵を設定したユーザ名に変更する
4. `mv hosts.sample hosts` を実行し、[default] の設定を対象のホストに変更する
5. `ansible all -m ping` で疎通確認

5 が成功したら OK
