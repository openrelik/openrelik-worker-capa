# Openrelik worker openrelik-worker-capa

## Description

Identify capabilities in executable files

## Deploy

Add the below configuration to the OpenRelik docker-compose.yml file.

```
openrelik-worker-openrelik-worker-capa:
    container_name: openrelik-worker-openrelik-worker-capa
    image: ghcr.io/openrelik/openrelik-worker-openrelik-worker-capa:latest
    restart: always
    environment:
      - REDIS_URL=redis://openrelik-redis:6379
      - OPENRELIK_PYDEBUG=0
    volumes:
      - ./data:/usr/share/openrelik/data
    command: "celery --app=src.app worker --task-events --concurrency=4 --loglevel=INFO -Q openrelik-worker-openrelik-worker-capa"
```

## Test

```
pip install poetry
poetry install --with test --no-root
poetry run pytest --cov=. -v
```
