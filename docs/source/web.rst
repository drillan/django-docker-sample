Webサーバコンテナの作成
========================

ここからは本番環境を想定し、WebサーバとしてNginxのコンテナを追加します。

ディレクトリとファイルを作成します。

.. code-block:: bash

   mkdir -p docker/web/conf.d
   touch docker/web/conf.d/default.conf
   touch docker/.env.prod
   touch docker-compose.prod.yml

.. literalinclude:: ../../docker/web/conf.d/default.conf
   :linenos:
   :caption: ``docker/web/conf.d/default.conf``

.. literalinclude:: ../../docker/.env.prod
   :linenos:
   :caption: ``docker/.env.prod``

.. literalinclude:: ../../docker-compose.prod.yml
   :language: yaml
   :linenos:
   :caption: ``docker-compose.prod.yml``

コンテナを起動します。

.. code-block:: bash

   docker compose -f docker-compose.prod.yml up -d

コンテナが起動していることを確認します。

.. code-block:: bash

   docker compose -f docker-compose.prod.yml ps

.. code-block::

   NAME                IMAGE                      COMMAND                  SERVICE             CREATED             STATUS                    PORTS
   django              django-docker-sample-app   "poetry run gunicorn…"   app                 32 minutes ago      Up 32 minutes             0.0.0.0:8000->8000/tcp, :::8000->8000/tcp
   mysql               mysql:8                    "docker-entrypoint.s…"   db                  32 minutes ago      Up 32 minutes (healthy)   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp
   nginx               nginx                      "/docker-entrypoint.…"   web                 32 minutes ago      Up 32 minutes             0.0.0.0:80->80/tcp, :::80->80/tcp

ログにエラーがないことを確認します。

.. code-block:: bash

   docker compose -f docker-compose.prod.yml logs

マイグレーションファイルを生成します。

.. code-block:: bash

   docker compose -f docker-compose.prod.yml exec app poetry run python manage.py makemigrations

マイグレーションを実行します。

.. code-block:: bash

   docker compose -f docker-compose.prod.yml exec app poetry run python manage.py migrate

`http://localhost/polls/ <http://localhost/polls/>`_ にアクセスできることを確認します。

コンテナを終了します。

.. code-block:: bash

   docker compose -f docker-compose.prod.yml down