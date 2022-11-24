

開発サーバー起動

```bash
./vendor/bin/sail up
```



シェル開く

```bash
./vendor/bin/sail root-shell
```



ER図の画像生成

```bash
php artisan generate:erd er.png
```


## 手順

Laravelプロジェクト作成。
```bash
curl -s https://laravel.build/laravel-app | bash
```

```bash
cd laravel-app
```


使うライブラリで`graphviz`のインストールが必要なので、Dockerfileを書き出す。

```bash
./vendor/bin/sail artisan sail:publish
```

書き出し後に、使っているバージョンのDockerfileを編集して、graphvizのインストールコマンドを追記する。  
`apt-get install -y graphviz`を追加した。

```bash
    && apt-get install -y postgresql-client-$POSTGRES_VERSION \
    && apt-get install -y graphviz \
    && apt-get -y autoremove \
    && apt-get clean \
```


シェルを開く。

```bash
./vendor/bin/sail root-shell
```

ライブラリ追加。
( `composer require beyondcode/laravel-er-diagram-generator --dev`だとエラー起きた)
https://github.com/beyondcode/laravel-er-diagram-generator/issues/93#issuecomment-1007517045

```bash
composer require beyondcode/laravel-er-diagram-generator --dev --ignore-platform-reqs -W
```


migrate

```bash
php artisan migrate
```


ER図を生成する。

```bash
php artisan generate:erd er.png
```
