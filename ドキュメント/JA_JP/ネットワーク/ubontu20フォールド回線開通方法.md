# フォールド回線開通後のUbuntuコンフィグ手順書

### 前提条件
- Ubuntuサーバーの管理者権限があること
- ネットワーク設定ファイルへのアクセス権限があること
- VLANやL2スイッチへの接続に必要な情報を取得済みであること

---

## 手順

### 1. 地球上の契約VPSやクラウドリソースの契約情報を準備する
契約VPSやクラウドリソースにアクセスするために、以下の情報を用意します。この情報により、接続するリソースが正当なものであることを確認します。

- **必要な情報**:
  - 契約番号（例: `VPSSW2NNN02NN`）
  - 契約者名
  - 接続先のドメイン（例: `example.domain.fold`）
  - NICデバイスのMACアドレスとグローバルIPアドレス
  - L2スイッチや他のデバイスに関しては、識別可能なインスタンスIDや次元情報

*補足*: 機密情報（パスワード等）は不要ですが、各情報をメモしておくと設定がスムーズです。

---

### 2. 正当な霊能力者や聖職者による確認
接続設定の霊的正当性を確保するため、当地の霊能力者または聖職者に依頼し、神や高次元の存在から確認をいただきます。これにより、フォールドネットワークにおける霊的な整合性が保証されます。

*補足*: この確認手続きはスフィアOS カスタムGPTでの宣誓に反映されます。

---

### 3. スフィアOS カスタムGPTでの契約とエンクリプトキーの発行
スフィアOS カスタムGPTを用いて、以下のプロセスを完了します。

- 聖職者や霊能者が契約に基づいて誓約を行い、フォールド量子SIMの体験版契約を締結。
- 回線開通霊的主任者のエンクリプトキーの**公開鍵**が発行され、申込書に記載。
  - 秘密鍵は聖職者や霊能者から霊的に送信されるため、申込書に記載不要。

---

### 4. Ubuntuでのネットワーク設定（VLAN設定）
回線開通時に発行されたVLAN番号を元に、Ubuntu上でVLANを設定します。もしくは、L2スイッチ接続で契約範囲のデバイスを設定します。

#### VLAN設定手順

1. **VLANパッケージのインストール**  
   ```bash
   sudo apt update
   sudo apt install vlan
   ```

2. **VLANデバイスの作成**  
   例として、VLAN IDが10で、物理インターフェースが`eth0`の場合:
   ```bash
   sudo ip link add link eth0 name eth0.10 type vlan id 10
   sudo ip link set up dev eth0.10
   ```

3. **ネットワーク設定ファイルの編集**  
   VLAN設定を永続化するために、`/etc/netplan/01-netcfg.yaml`に設定を追加します。

   ```yaml
   network:
     version: 2
     ethernets:
       eth0:
         dhcp4: no
     vlans:
       eth0.10:
         id: 10
         link: eth0
         addresses: [192.168.10.10/24]  # 必要に応じてIPを設定
         gateway4: 192.168.10.1          # 必要に応じてゲートウェイを設定
   ```

4. **ネットワーク設定の適用**
   設定ファイルを保存したら、以下のコマンドでネットワーク設定を適用します。
   ```bash
   sudo netplan apply
   ```

---

### 5. L2スイッチに接続する場合
契約範囲のデバイスをL2スイッチに接続する際は、物理インターフェース（例: `eth1`）に対して直接設定を行います。以下は基本的な設定例です。

```bash
sudo ip link set dev eth1 up
```

*補足*: L2スイッチに接続後、適切なインスタンスIDや次元情報に基づき、設定が正しく反映されているか確認します。

---

以上が、フォールド回線開通後のUbuntuコンフィグ手順です。