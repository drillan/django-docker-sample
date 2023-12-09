環境構築
=========

`公式ドキュメント <https://python-poetry.org/docs/>`_ に従ってPoetryのインストールをします。

  https://python-poetry.org/docs/#installing-with-the-official-installer

プロジェクトを生成します。

.. code-block:: bash

   poetry init -q --name mysite

仮想環境に入ります。

.. code-block:: bash

   poetry shell 

パッケージを追加します。

.. code-block:: bash

   poetry add Django=4.2 mysqlclient gunicorn

