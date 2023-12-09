Djangoアプリケーションの作成
===============================

ここでは、 `Django公式ドキュメント - はじめての Django アプリ作成 <https://docs.djangoproject.com/ja/5.0/intro/tutorial01/>`_ に従ってアプリケーションを作成します。

プロジェクトを作成します。

.. code-block:: bash

   django-admin startproject mysite

アプリケーションを作成します。

.. code-block:: bash

   python manage.py startapp polls

次のファイルを追加/編集します。

``polls/views.py``

.. literalinclude:: ../../mysite/polls/views.py
   :language: python
   :linenos:

``polls/urls.py``

.. literalinclude:: ../../mysite/polls/urls.py
   :language: python
   :linenos:

``mysite/urls.py``

.. literalinclude:: ../../mysite/mysite/urls.py
   :language: python
   :linenos:

``polls/models.pys``

.. literalinclude:: ../../mysite/polls/models.py
   :language: python
   :linenos:

``mysite/mysite/settings.py``

.. literalinclude:: ../../mysite/mysite/settings.py
   :language: python
   :lines: 37-45
   :emphasize-lines: 2

開発サーバを起動し、 `http://localhost:8000/polls/ <http://localhost:8000/polls/>`_ にアクセスできることを確認します。

.. code-block:: bash

   python manage.py runserver