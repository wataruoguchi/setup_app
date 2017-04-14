FROM python:3.5
ENV PYTHONUNBUFFERED 1
RUN mkdir /src
ADD ./app/src /src/
RUN mkdir /config
ADD ./app/requirements.txt /config/
RUN pip install -r /config/requirements.txt
WORKDIR /src
