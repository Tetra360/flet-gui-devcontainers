FROM ubuntu:22.04

# 基本設定
RUN apt-get update && \
    apt-get install -y \
        locales \
        fonts-noto-cjk \
        gedit && \
            locale-gen ja_JP.UTF-8 && \
            update-locale LANG=ja_JP.UTF-8


# 必要なパッケージをインストール
RUN apt-get update && \
    apt-get install -y \
        python3 \
        python3-pip \
        x11-apps \
        libgtk-3-0 \
        gstreamer1.0-plugins-base \
        libmpv1 && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 環境変数を日本語に設定
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=ja_JP:ja
ENV LC_ALL=ja_JP.UTF-8

# 作業ディレクトリを設定
WORKDIR /app
# COPY /app /app/app
# requirements.txtをコピー
COPY requirements.txt ./

# すべてroot権限で実行 (fletuserは削除)
# ディレクトリ権限をrootで変更
RUN chown -R root:root /app

# 依存パッケージのインストール
RUN pip install --no-cache-dir -r requirements.txt

# ~/.local/binをPATHに追加 (pipで--userオプションを使った場合のインストール先)
ENV PATH="/root/.local/bin:$PATH"

CMD ["python", "/app/main.py"]