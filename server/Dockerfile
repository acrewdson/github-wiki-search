FROM python:2

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install gcc \
    make g++ ca-certificates zlib1g-dev libffi-dev \
    libxml2 libxslt1-dev libxslt-dev libxml2-dev

ADD . /app

WORKDIR /app

RUN pip install -r requirements.txt

CMD ["python", "--version"]

# TODO figure out entrypoint
