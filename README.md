# forta
- Install(chung update)
sudo curl https://dist.forta.network/pgp.public -o /usr/share/keyrings/forta-keyring.asc -s
echo 'deb [signed-by=/usr/share/keyrings/forta-keyring.asc] https://dist.forta.network/repositories/apt stable main' | sudo tee -a /etc/apt/sources.list.d/forta.list
sudo apt-get update
sudo apt-get install forta

-Tạo Service

sudo tee /etc/systemd/system/fortad.service > /dev/null <<EOF
[Unit]
Description=Forta Node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/
ExecStart=$(which forta) run --passphrase=Cugkodc1
Restart=on-failure
RestartSec=3
LimitNOFILE=10000

[Install]
WantedBy=multi-user.target
EOF

nhớ đổi passphrase của bác

systemctl daemon-reload
systemctl enable fortad
systemctl restart fortad && journalctl -n 100 -f -u fortad -o cat
