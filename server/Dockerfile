FROM python:2

ENV ES_HOST http://elasticsearch:9200/
ENV GH_AUTH_TOKEN gh_auth_token
ENV GH_ORG gh_org
ENV GH_USER gh_user
ENV GHE_AUTH_TOKEN ghe_auth_token
ENV GHE_HOST http://ghe/
ENV GHE_USER ghe_user
ENV JIRA_HOST https://jira/

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install gcc \
    make g++ ca-certificates zlib1g-dev libffi-dev \
    libxml2 libxslt1-dev libxslt-dev libxml2-dev

ADD . /app/server

WORKDIR /app/server

RUN pip install -r requirements.txt

RUN curl -o /usr/local/bin/mantra -L \
    https://github.com/acrewdson/mantra/releases/download/0.0.2/mantra && \
    chmod +x /usr/local/bin/mantra

ENV PYTHONPATH=$PYTHONPATH:/app

WORKDIR /app

# run indexing at 5 am every morning
CMD ["/usr/local/bin/mantra", "01 01 05 * * *", "python", "/app/server/index.py"]
