FROM python:3.12-slim

ARG SWA_BERT_VERSION
ENV PYTHONUNBUFFERED 1

WORKDIR /app

RUN apt-get update && apt-get install -y build-essential redis libpq-dev \
  && pip install --upgrade pip supervisor \
  && python --version \
  && pip install swa-bert==${SWA_BERT_VERSION} \
  && apt-get autoremove -y build-essential \
  && mkdir -p /data/db

COPY supervisord.conf /etc/supervisord.conf

ENV DATABASE_LOCATION=/data/db
ENV SECRETS_DIR /run/secrets

ENV PORT=80
EXPOSE ${PORT}

CMD ["supervisord", "-c", "/etc/supervisord.conf"]
