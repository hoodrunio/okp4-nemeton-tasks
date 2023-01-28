# Imbolg tasks

## Expose RPC node

Submission form: https://okp4.typeform.com/Nemeton-RPC

**DO NOT perform these steps on your validator node!**

```bash
sudo apt install make clang pkg-config libssl-dev build-essential git jq ncdu nload -y < "/dev/null"

ver="1.19.3"
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
go version
```

```bash
git clone https://github.com/okp4/okp4d
cd okp4d
```

```bash
make install
okp4d version

# the output should be v3.0.0
```

```bash
MONIKER="RPC"
CHAIN_ID="okp4-nemeton-1"

okp4d init $MONIKER --chain-id $CHAIN_ID
wget https://raw.githubusercontent.com/okp4/networks/main/chains/nemeton-1/genesis.json -O $HOME/.okp4d/config/genesis.json
```

```bash
sudo tee <<EOF >/dev/null /etc/systemd/system/okp4d.service
[Unit]
Description=okp4d daemon
After=network-online.target

[Service]
User=$USER
ExecStart=$(which okp4d) start
Restart=always
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
EOF

cat /etc/systemd/system/okp4d.service
sudo systemctl enable okp4d
sudo systemctl daemon-reload
sudo systemctl start okp4d
```

```bash
PEERS=a6fc531f7274aa6615fa33198496ea69b2023a0f@144.76.90.130:29656,61544968b65e34a59513b67613519cd37ace7ecb@161.97.151.109:26656,9480ac9cfc118a571741bd75d477a5308a19fe0a@136.243.103.32:36656,8527f34bd6e542304809386896997d12d80e5e0e@65.108.237.232:29656,2e85c1d08cfca6982c74ef2b67251aa459dd9b2f@65.109.85.170:43656,264256d32511c512a0a9d4098310a057c9999fd1@65.21.90.141:12234,d5519e378247dfb61dfe90652d1fe3e2b3005a5b@65.109.68.190:36656,14f8949ab0a276d2e55c8fa6255430881978a619@185.192.96.236:26656,639f8d9ac9c03159f7366f8f83cd3b46de51c735@135.181.176.109:53656,55e47b6700f598afb5da528f503c2beaedfd1b59@176.103.222.45:26656,f7e481df45bfbe62ea0553f5f6da34eaf4f688c3@194.34.232.225:26656,6470a3088ff58d22e4b271e52c1d73c1ceb5d798@159.148.146.132:26656,26114bc5cb42ef90be2aba5b4b6d82bab7a60c31@185.255.131.17:26656,428821d6b64eee5d67da467a4673ce2b1e52955d@54.88.179.178:26656,cee007d27c78754ae63ed827e61c8a920192f54b@65.109.93.152:28656,0c05d3f9c166028ffb3a2ce60bfbeeb55031ec43@23.88.55.152:11204,e676fad27d970abede25b0469676b05ea83e5f04@144.168.47.230:36656,5c2a752c9b1952dbed075c56c600c3a79b58c395@95.214.55.232:26996,307fb25cd6998d0d5bd1d947571f6043c6bb4069@65.109.31.114:2280,d1a0ff9bd7ea1ebd06bc7158f3523f5e557328be@163.172.131.169:26656,1655cdc8fdfe1dc2209d47ff68c02a417ef9ed52@135.181.222.179:31656,4ea26ce893d8f4f89a7b49b9bd77e0fbd914e029@65.109.88.162:36656,d4305fcb7b20dc96481a6ae6ae84f281f3413a4e@65.109.37.58:13656,e755eb8016c2f6f5303b2f8d503d9126d235e80f@138.201.35.56:26656,0448864ede56d3c96d7d3bb8ea9f546b70cc722e@51.159.149.68:26656,7a15c08f8552d99346976b485d071ce0faa52ed3@65.108.78.80:30656,a7bb3eb07cd22f9d96b54d61e2b4b3f2bfe33cf0@65.109.188.119:46656,945adec41a9ebec8e3df76a6c08efda33d0852db@69.197.7.30:20621,a009a02a23428538b57591f73ba5a6462c476a70@136.243.88.91:6040,30092d2717053f1c0813e8354c07c761c9c3ac5c@194.163.161.234:26656,9f55b6fbf5d246138cc88acfe193ac45aa49c288@31.7.196.148:26656,23e895e7d650f43e1f53522165607b71685f8cfa@65.108.75.107:26656,2bfd405e8f0f176428e2127f98b5ec53164ae1f0@142.132.149.118:26656,61a8b9fdd5c21ebe6c02359cb192a4eda13d44cb@135.181.139.153:26656,540e0e9b33b2d87315fdf7089404671581d36e94@95.217.203.43:26656,b0b56d944cf1cc569a1e77e0923e075bad94d755@141.95.145.41:28656,d7d3e978951ccf946f0e33805778c1961ad42819@31.7.196.21:26656,24fbac02738005cfa9d8263d01dc7cc113d6b708@162.248.225.244:26656,8028015d1c6828a0b734f3b108f0853b0e19305e@157.90.176.184:26656,8a7605d8ae4338de5b7a0d5c70244ce05e377630@85.10.200.221:26656,717425f8bcbd75d6e13a40e76ec3863ef1a89cda@38.242.216.50:26656,f74f793a1efa51778fd74d4dbc5a1e88a8c644db@116.202.227.117:36656,9689dcc3ab9026265950a5a7040c55ad1ce6b003@65.108.69.68:27363,2ca4e1bed94cfe9fad160e704ccbabf95f438dee@65.108.129.29:60656,79fd122745c37cc4abe225796a20d121e4cbf9e4@135.181.215.62:6070,3d8c31caa0c1737e642aee41542a579dd727eb0b@109.123.243.135:13656,a49302f8999e5a953ebae431c4dde93479e17155@141.95.153.244:26656,4fab49bfc0ad6d02dc92f8a9a5551c324e30a6fb@65.108.97.58:36656,f3cccec7bdba9d5d4bd156087e3c6e2e5aa42948@65.108.134.215:29656,38b8e30bb805cca8358b28f1bd7b8177cbbf1ec3@65.108.236.195:26656,907afed8fb7561b6d9bc6f755c8e4cce52e55080@65.108.72.252:26656,c3db3a07493e8f04d93a9228998ae799fa89877f@5.78.48.118:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.okp4d/config/config.toml

SNAP_RPC="https://okp4-testnet-rpc.polkachu.com:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.okp4d/config/config.toml

sudo systemctl stop okp4d
okp4d tendermint unsafe-reset-all --home $HOME/.okp4d --keep-addr-book
sudo systemctl start okp4d
```

Wait for sync. then;

```bash
PORTR=$(grep -A 3 "\[rpc\]" ~/.okp4d/config/config.toml | egrep -o ":[0-9]+")
sed -i.bak -e "s%^laddr = \"tcp://127.0.0.1$PORTR\"%laddr = \"tcp://0.0.0.0$PORTR\"%" $HOME/.okp4d/config/config.toml
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" $HOME/.okp4d/config/config.toml
systemctl restart okp4d
```

Get your RPC URL:
```bash
echo $(curl -s -4 ifconfig.me)$PORTR
```


## Provide snapshots

**Submission form: https://okp4.typeform.com/NemetonSnapshot**

```bash
mkdir -p $HOME/snapshot/testnet/okp4
```

```bash
sudo apt-get install nginx -y
sudo unlink /etc/nginx/sites-enabled/default
```

```bash
sudo tee <<EOF >/dev/null /etc/nginx/sites-available/file-server.conf
server {
    listen       80;
    client_max_body_size 5G;
    proxy_max_temp_file_size 0;
    root /root/snapshot/;
    autoindex on;
}
EOF
sudo ln -s /etc/nginx/sites-available/file-server.conf /etc/nginx/sites-enabled/file-server.conf
chmod o+x /root/snapshot
chmod o+x /root/
service nginx restart
```

```bash
wget https://raw.githubusercontent.com/testnetrunn/okp4-nemeton-tasks/main/snapshot.sh

bash snapshot.sh
EOF
```

Get your snapshot URL:

```bash
echo http://$(curl -s -4 ifconfig.me)/testnet/okp4
```

## Provide dashboard for the OKP4 network

## Tweet about the uptime war

## Uptime war: prevent getting jailed!

