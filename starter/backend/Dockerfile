FROM python:3.10-alpine3.18

RUN adduser -u 1000 -D app

RUN apk update && \
    apk add --no-cache \
    pcre \
    pcre-dev \
    build-base \
    linux-headers \
    openssl \
    libffi-dev \
    && pip install --no-cache-dir pipenv

WORKDIR /app

COPY Pipfile* /app/

RUN pipenv install --system --deploy

COPY . /app

EXPOSE 5000

USER app

CMD ["uwsgi", "--ini", "/app/uwsgi.ini"]
