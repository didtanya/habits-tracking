FROM python:3.11

# Disables the buffer for instant output of messages to stdout from processes.
ENV PYTHONUNBUFFERED=1

# Install system requires
RUN apt-get update && \
    apt-get install -y --no-install-recommends libpq5 wait-for-it python3-cffi && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/*

## Install poetry
RUN pip install --no-cache-dir poetry

WORKDIR /app/src

COPY pyproject.toml poetry.lock /app/src/

## Install app requires
RUN poetry config experimental.new-installer false
RUN poetry config virtualenvs.create false && \
    poetry install --no-interaction --no-ansi

COPY ./ /app/src/

# Move scripts to /app
RUN find . -name '*.sh' -exec mv '{}' /app/ \;
RUN poetry install --no-dev
