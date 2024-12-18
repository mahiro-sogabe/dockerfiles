# forAwsLambdaLayer

Lambdaのレイヤーで使用するPythonライブラリを作成する環境を構築します。

## 構築内容

- Python 3.12.7
- AWS CLI

## 実行方法

### Dockerイメージのビルド

```bash
docker build -t my-python-env .
```

### コンテナ起動

コンテナをマウントしていないので、コンテナから抜けるとデータは削除される。

```docker
docker run -it --rm my-python-env
```

### AWSアカウントのプロファイル登録


```bash
aws configure
```

### レイヤーに追加するライブラリインストール

インストールするライブラリについては適宜合わせる。

```bash
mkdir python && cd python
```

```bash
pip install awsiotsdk==1.22.1 -t .
```

```bash
zip -r python.zip python
```

### デプロイ

```bash
aws lambda publish-layer-version \
    --layer-name forIotCore \
    --zip-file fileb://python.zip \
    --compatible-runtimes python3.12
```