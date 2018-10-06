FROM python:3.5
RUN apt-get update && apt-get install -y \
  gcc \
  gettext \
  postgresql-client libpq-dev \
  sqlite3 \
  --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src/{{ cookiecutter.repo_name }}
WORKDIR /usr/src/{{ cookiecutter.repo_name }}

ADD requirements.txt /usr/src/{{ cookiecutter.repo_name }}/
RUN pip install --no-cache-dir -r requirements.txt
ADD README.txt CHANGES.txt MANIFEST.in setup.py /usr/src/{{ cookiecutter.repo_name }}/
RUN pip install -e . && pip install -e ".[testing]"
ADD development.ini /usr/src/{{ cookiecutter.repo_name }}/

ADD {{ cookiecutter.repo_name }} /usr/src/{{ cookiecutter.repo_name }}/{{ cookiecutter.repo_name }}
RUN initialize_{{ cookiecutter.repo_name }}_db development.ini

EXPOSE 6543
CMD pserve development.ini --reload