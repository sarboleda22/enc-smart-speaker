FROM python:3.7-alpine

LABEL maintainer="Sebastian Arboleda <sebasarboleda22@gmail.com"
LABEL Name=talking_cub_webapp
LABEL Version=0.0.1

EXPOSE 8000

COPY ./requirements/requirements.txt /

RUN apk add --no-cache postgresql-libs \
    && apk add --no-cache --virtual .build-deps gcc musl-dev postgresql-dev \
    && python3 -m pip install -r requirements.txt --no-cache-dir \
    && apk --purge del .build-deps

COPY ./run.py /
COPY ./webapp /webapp
WORKDIR /

CMD [ "gunicorn", "-w", "4", "-b", "0.0.0.0:8000", "--access-logfile", "-", "--error-logfile", "-", "run:app" ]
