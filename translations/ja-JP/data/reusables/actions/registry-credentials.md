イメージのコンテナレジストリがイメージをプルするために認証を要求するなら、`username`と`password`の`map`を設定するために`jobs.<job_id>.container.credentials`が利用できます。 この認証情報は、[`docker login`](https://docs.docker.com/engine/reference/commandline/login/)コマンドに渡すものと同じ値です。