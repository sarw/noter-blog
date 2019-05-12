# mixhostにperlbrew、cpanm、cartonなどをインストールする
<!-- date:2019-05-10 02:49:43 -->

## perlbrewのインストール

``` bash
curl -L https://install.perlbrew.pl | bash
```

その後、以下を実行したのちにログインし直す

``` bash
echo "source ~/perl5/perlbrew/etc/bashrc" >> ~/.bash_profile
```

## cpanmのインストール

``` bash
perlbrew install-cpanm
```

## cartonのインストール

