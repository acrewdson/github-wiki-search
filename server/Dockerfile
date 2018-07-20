FROM python:2

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install gcc \
    make g++ ca-certificates zlib1g-dev libffi-dev \
    libxml2 libxslt1-dev libxslt-dev libxml2-dev

ADD . /app/server

WORKDIR /app/server

RUN pip install -r requirements.txt

RUN curl -o /usr/local/bin/mantra -L \
    https://github.com/pugnascotia/mantra/releases/download/0.0.1/mantra && \
    chmod +x /usr/local/bin/mantra

ENV PYTHONPATH=$PYTHONPATH:/app

WORKDIR /app

# run indexing at 03:00 each day
CMD ["/usr/local/bin/mantra", "0 3 * * * *", "python", "/app/server/index.py"]
