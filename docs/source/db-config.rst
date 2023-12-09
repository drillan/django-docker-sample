データベースの設定
==================

``mysite/mysite/settings.py`` を追加/編集します。

.. literalinclude:: ../../mysite/mysite/settings.py
   :language: python
   :lines: 13-14
   :emphasize-lines: 2
   :caption: ``mysite/mysite/settings.py``

.. literalinclude:: ../../mysite/mysite/settings.py
   :language: python
   :lines: 24-32
   :emphasize-lines: 2,6,9
   :caption: ``mysite/mysite/settings.py``

.. literalinclude:: ../../mysite/mysite/settings.py
   :language: python
   :lines: 88-101
   :emphasize-lines: 3-11
   :caption: ``mysite/mysite/settings.py``

``docker-compose.dev.yml`` を編集し、データベース起動後にアプリケーションが起動するようにします。

.. literalinclude:: ./code/docker-compose.dev3.yml
   :language: yaml
   :linenos:
   :emphasize-lines: 11-13,24-29
   :caption: ``docker-compose.dev.yml``

コンテナを起動します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml up -d

コンテナが起動していることを確認します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml ps

.. code-block::

   NAME                IMAGE                      COMMAND                  SERVICE             CREATED             STATUS                   PORTS
   django              django-docker-sample-app   "poetry run python m…"   app                 6 minutes ago       Up 6 minutes             0.0.0.0:8000->8000/tcp, :::8000->8000/tcp
   mysql               mysql:8                    "docker-entrypoint.s…"   db                  6 minutes ago       Up 6 minutes (healthy)   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp

ログにエラーがないことを確認します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml logs

マイグレーションファイルを生成します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml exec app poetry run python manage.py makemigrations

.. code-block::

   Migrations for 'polls':
   polls/migrations/0001_initial.py
      - Create model Question
      - Create model Choice

マイグレーションを実行します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml exec app poetry run python manage.py migrate


.. code-block::

   Operations to perform:
   Apply all migrations: admin, auth, contenttypes, polls, sessions
   Running migrations:
   Applying contenttypes.0001_initial... OK
   Applying auth.0001_initial... OK
   Applying admin.0001_initial... OK
   Applying admin.0002_logentry_remove_auto_add... OK
   Applying admin.0003_logentry_add_action_flag_choices... OK
   Applying contenttypes.0002_remove_content_type_name... OK
   Applying auth.0002_alter_permission_name_max_length... OK
   Applying auth.0003_alter_user_email_max_length... OK
   Applying auth.0004_alter_user_username_opts... OK
   Applying auth.0005_alter_user_last_login_null... OK
   Applying auth.0006_require_contenttypes_0002... OK
   Applying auth.0007_alter_validators_add_error_messages... OK
   Applying auth.0008_alter_user_username_max_length... OK
   Applying auth.0009_alter_user_last_name_max_length... OK
   Applying auth.0010_alter_group_name_max_length... OK
   Applying auth.0011_update_proxy_permissions... OK
   Applying auth.0012_alter_user_first_name_max_length... OK
   Applying polls.0001_initial... OK
   Applying sessions.0001_initial... OK

コンテナを終了します。

.. code-block:: bash

   docker compose -f docker-compose.dev.yml down