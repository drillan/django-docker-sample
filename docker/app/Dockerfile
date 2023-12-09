FROM python:3.11

RUN apt-get update && \
    apt-get install -y curl default-libmysqlclient-dev build-essential pkg-config

RUN adduser django && \
    usermod -aG www-data django

USER django
RUN curl -sSL https://install.python-poetry.org | python3 -
COPY --chown=django:django ./mysite /home/django/mysite
COPY --chown=django:django ./pyproject.toml /home/django/pyproject.toml
WORKDIR /home/django
ENV PATH="/home/django/.local/bin:$PATH"
RUN poetry install

WORKDIR /home/django/mysite