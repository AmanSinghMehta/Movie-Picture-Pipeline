FROM public.ecr.aws/docker/library/python:3.10-alpine

RUN adduser -u 1000 -D app

RUN apk update && \
    apk add \
    pcre \
    pcre-dev \
    build-base \
    gcc \
    linux-headers \
    openssl \
    libffi-dev \
    && pip install pipenv

# Force GCC to treat legacy C pointer signatures as warnings, not fatal errors
ENV CFLAGS="-Wno-error=incompatible-pointer-types"
ENV CPPFLAGS="-Wno-error=incompatible-pointer-types"

RUN mkdir -p /var/www/app && mkdir /app

WORKDIR /app

COPY Pipfile* /app/
RUN pipenv install --system --deploy

COPY . /app

EXPOSE 5000

USER app

CMD ["uwsgi", "--ini", "/app/uwsgi.ini"]
