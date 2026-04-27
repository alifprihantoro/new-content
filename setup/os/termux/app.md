## install
> [!WARNING]
> mungkin ada app yang tidak kalian butuhkan, jadi silahkan pilih app yang ingin kalian install
```sh
pkg update -y
pkg upgrade -y
# install cli tools
pkg install bat gh git zsh lsd fzf tmux ripgrep termux-api yq which make man aria2 htop clang -y
# security apps
pkg install openssh -y
# install glibc
pacman -S glibc-runner
# install db
pkg install postgresql mariadb mongodb -y
# install language and related tools
pkg install nodejs esbuild golang rust php composer python python-pip -y
# use main because latest ver. have bug for pnpm
go install github.com/google/osv-scanner/cmd/osv-scanner@main
# install pnpm
npm i -g pnpm                                                
# tools live server
Ppnpm i -g live-server                                        
# install wordpress
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
mv wp-cli.phar ~/../usr/bin/wp

```
### bun
> [!IMPORTANT]
> change `aria2c` to `curl/wget` if you not installed yet
```sh
# install bun
aria2c -x5 https://github.com/oven-sh/bun/releases/latest/download/bun-linux-aarch64.zip bun.zip
unzip bun.zip
mkdir -p ~/.bun/bin
mv bun/bun ~/.bun/bin
rm -rf bun
echo '#!/bin/sh\ngrun ~/.bun/bun $@' >~/../usr/bin/bun
chmod +x ~/../usr/bin/bun
```
### lsp
see [here](../nvim.md#install-lsp)
