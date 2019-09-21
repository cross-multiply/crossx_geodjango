FROM python:3.7-alpine

ENV PYTHONUNBUFFERED 1


RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" > /etc/apk/repositories \
    && echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && echo "http://mirror.leaseweb.com/alpine/edge/testing" >> /etc/apk/repositories


RUN apk update \
    # psycopg2 dependencies
    && apk add --virtual build-deps g++ python3-dev musl-dev \
    && apk add postgresql-dev \
    # Pillow dependencies
    && apk add jpeg-dev zlib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev \
    # CFFI dependencies
    && apk add libffi-dev py-cffi \
    # Translations dependencies
    && apk add gettext \
    # https://docs.djangoproject.com/en/dev/ref/django-admin/#dbshell
    && apk add postgresql-client \
    && apk add expat geos geos-dev giflib libcrypto1.1 libcurl libgcc libjpeg-turbo libpng libpq libstdc++ sqlite-libs \
    && apk add gdal gdal-dev 

# && apk add --update-cache --no-cache py3-scipy py3-numpy cython
#Requirements are installed here to ensure they will be cached.
ENV PYTHONPATH=/usr/lib/python3.7/site-packages



# RUN wget https://bootstrap.pypa.io/get-pip.py && python3.7 get-pip.py && rm get-pip.py
#RUN pip install --no-cache-dir setuptools wheel -U


COPY ./requirements /requirements
RUN pip install -r /requirements/local.txt

COPY ./docker/production/django/entrypoint /entrypoint
RUN sed -i 's/\r$//g' /entrypoint
RUN chmod +x /entrypoint

COPY ./docker/local/django/start /start
RUN sed -i 's/\r$//g' /start
RUN chmod +x /start

# COPY ./docker/local/django/celery/worker/start /start-celeryworker
# RUN sed -i 's/\r$//g' /start-celeryworker
# RUN chmod +x /start-celeryworker

# COPY ./docker/local/django/celery/beat/start /start-celerybeat
# RUN sed -i 's/\r$//g' /start-celerybeat
# RUN chmod +x /start-celerybeat

# COPY ./docker/local/django/celery/flower/start /start-flower
# RUN sed -i 's/\r$//g' /start-flower
# RUN chmod +x /start-flower

WORKDIR /app

ENTRYPOINT ["/entrypoint"]
