FROM python:3.5
RUN mkdir -p /usr/src/{{ cookiecutter.repo_name }}
WORKDIR /usr/src/{{ cookiecutter.repo_name }}
RUN apt-get update && apt-get install -y \
  gcc \
  gettext \
  postgresql-client libpq-dev \
  sqlite3 \
  --no-install-recommends && rm -rf /var/lib/apt/lists/*
COPY requirements.txt /usr/src/{{ cookiecutter.repo_name }}/
RUN pip install --no-cache-dir -r requirements.txt
COPY README.txt CHANGES.txt MANIFEST.in setup.py /usr/src/{{ cookiecutter.repo_name }}/
RUN pip install -e . && pip install -e ".[testing]"
COPY . /usr/src/{{ cookiecutter.repo_name }}
RUN initialize_{{ cookiecutter.repo_name }}_db development.ini
EXPOSE 6543
CMD pserve development.ini --reload