<h1>My Docker Wiki</h1>
<h3>Docker 起動</h3>

```
$docker run image-name
```
</br>
起動の動作:DockerクライアントからDockerデーモン中にImage探す、なければDocker Hubをダウンロードする。
</br>
docker run : docker pull(イメージを取る) + docker create(イメージの作成)+docker start(コンテナの起動)
<h3>コンテナで呼び出すコマンド</h3>

```
$docker run username/image-name cowsay Hello!
```
</br>
cowsay:コンテナで呼び出すコマンド
<h3>ダウンロード済み一覧</h3>

```
$docker images
```

<h3>イメージにタグつけするコマンド</h3>

```
$docker tag source_image-name:tag_name new_image_name
          
```
<h3>イメージの詳細情報を表示するコマンド</h3>

```
$docker inspect image-name
```

<h3>ローカルのイメージを削除するコマンド</h3>

```
$docker rmi username/image-name(imageID)
```
強制削除する場合は-fをつける

```
$docker rmi　-f usename/image-name(imageID)
```

<h3>イメージを取得</h3>

```
$docker pull username/image-name
```

<h2>Dockerfile</h2>
イメージは127 RUNステープ制限！

``` Dockerfile
#コメント
#イメージ導入
FROM username/image-name  
#開発者の情報
MAINTAINER 
LABEL description="" version="1.0" owner=""

RUN apt-get -y update && apt-get install -y  package-name
#コンテナ起動動作
#build時他のRUNある場合は実行しない
CMD　command param1 param2 
#build時他のRUNあるでも場合は実行する
ENTRYPOINT command param1 param2

#本機のファイルをコービしてイメージに指定のパースに保存する
COPY file1.txt file2.js file3.json ./mypath

#本機とURLのファイルをコービをイメージに指定のパースに保存する
ADD [–chown=<user>:<group>] <src>… <dest>
ADD file1.txt file2.js file3.json ./
ADD https://www.google.com/demo.gzip $ENV_DEMO_VALUE

#インタネットポート設定
EXPOSE <port> [<port>/<protocol>…]
#インタネットポート起動
docker run -p 80:80/tcp -p 80:80/udp demo
#インタネットポート全部起動
docker run -P demo

#環境変数設定
ENV demoPATH="" demoVer=""

#本機と別のコンテナはらのダウンロードどころ
VOLUME /var/log /var/db
#カレントディレクトリ
WORKDIR /a
WORKDIR b
WORKDIR c
RUN pwd
# /a/b/c

#ユーザー名付け
RUN groupadd -r tester && useradd -r -g tester tester
User tester

#イメージbuild時パラメタ入る
ARG Param1
ARG Param2=somevalue
docker build --build-arg Param1=demo -t myimage:v1 .

#ONBUILDはコンテナはベース指定する場合は実行する
ONBUILD ADD ./home/tmp
ONBUILD mkdir -p /home/demo/docker
FROM A-Image
#以下は自動実行する
ADD . /home/tmp
mkdir -p /home/demo/docker

```
参考サイト<br>
https://www.jinnsblog.com/2018/12/docker-dockerfile-guide.html
https://docs.docker.com/engine/reference/commandline/build/
