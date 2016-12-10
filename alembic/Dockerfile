FROM python:2.7
RUN apt-get update
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r requirements.txt
RUN  alembic init migration
ADD alembic.ini /usr/src/app/
