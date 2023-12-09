データベースコンテナの作成
===========================

MySQLデータベースコンテナを作成します。

ディレクトリとファイルを作成します。

.. code-block:: bash

   mkdir -p docker/db
   mkdir -p docker/db/conf.d
   mkdir -p docker/db/data
   touch docker/db/conf.d/my.conf
   touch docker/.env.dev

.. literalinclude:: ../../docker/db/conf.d/my.conf
   :linenos:
   :caption: ``docker/db/conf.d/my.conf``

.. literalinclude:: ../../docker/.env.dev
   :language: bash
   :linenos:
   :caption: ``docker/.env.dev``

``docker-compose.dev.yml`` に11-20行目を追加します。

.. literalinclude:: ./code/docker-compose.dev2.yml
   :language: yaml
   :linenos:
   :emphasize-lines: 11-20
   :caption: ``docker-compose.dev.yml``

データベースのコンテナを起動します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml up -d db

MySQLのデータベースに接続できることを確認します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml exec db mysqladmin ping -h 127.0.0.1 -uroot -p

コンテナを終了します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml down