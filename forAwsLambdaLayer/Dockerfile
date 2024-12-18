# Amazon Linux 2 イメージをベースにする
FROM amazonlinux:2

# 必要なパッケージをインストール
RUN yum update -y && \
    yum install -y gcc make patch zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl11-devel tk-devel libffi-devel xz-devel git zip tar && \
    yum install -y awscli

# pyenv のインストール
RUN curl https://pyenv.run | bash

# 環境変数を設定
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc && \
    echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc

# bashrc を読み込んで pyenv をインストール
RUN source ~/.bashrc && \
    pyenv install 3.12.7 && \
    pyenv global 3.12.7

# シェルを実行
CMD ["bash"]
