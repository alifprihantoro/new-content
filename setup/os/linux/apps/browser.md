## browser install

### chromium
```bash
apt-get install chromium -y
```
> [!IMPORTANT]
> for proot distro, execute this
```bash
rm /bin/chromium_real
mv /bin/chromium /bin/chromium_real
touch /bin/chromium
chmod +x /bin/chromium
cat >/bin/chromium <<EOF
#!/bin/bash
if [[ \$(id -u) -ne 0 ]]; then
  /bin/chromium_real \$@
else
  /bin/chromium_real --no-sandbox \$@
fi
EOF
```

### firefox
```bash
apt-get install firefox-esr -y
```
### brave
```bash
curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main" | tee /etc/apt/sources.list.d/brave-browser-release.list
apt update
apt install brave-browser -y
```
> [!IMPORTANT]
> for proot distro, execute this
```bash
# make brave use no sandbox as default
rm /bin/brave-browser-stable-bin
mv /bin/brave-browser-stable /bin/brave-browser-stable-bin
touch /bin/brave-browser-stable
chmod +x /bin/brave-browser-stable
cat >/bin/brave-browser-stable <<EOF
#!/bin/bash
if [[ \$(id -u) -ne 0 ]]; then
  /bin/brave-browser-stable-bin $@
else
  /bin/brave-browser-stable-bin --no-sandbox $@
fi
EOF

```
