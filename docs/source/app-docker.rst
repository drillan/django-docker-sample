アプリケーションコンテナの作成
==============================

Djangoアプリケーション用のDockerファイルを作成します。

.. code-block:: bash

   mkdir -p docker/app
   touch docker/app/Dockerfile
   trouch docker-compose.dev.yml


.. literalinclude:: ../../docker/app/Dockerfile
   :language: dockerfile
   :linenos:
   :caption: ``docker/app/Dockerfile``


.. literalinclude:: ./code/docker-compose.dev1.yml
   :language: yaml
   :linenos:
   :caption: ``docker-compose.dev.yml``

アプリケーションコンテナをビルドします。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml build app

アプリケーションコンテナを起動します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml up -d app

コンテナが起動していることを確認します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml ps

.. code-block::

   NAME                IMAGE                      COMMAND                  SERVICE             CREATED             STATUS                   PORTS
   django              django-docker-sample-app   "poetry run python m…"   app                 6 minutes ago       Up 6 minutes             0.0.0.0:8000->8000/tcp, :::8000->8000/tcp

ログにエラーがないことを確認します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml logs

`http://localhost:8000/polls/ <http://localhost:8000/polls/>`_ にアクセスできることを確認します。

コンテナを終了します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml down