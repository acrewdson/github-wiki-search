FROM elasticsearch:5.6.10

RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get install -y gcc 

RUN apt-get -y install python-pip
RUN apt-get -y install python-dev
RUN apt-get -y install libxslt-dev
RUN apt-get -y install git-core vim


RUN pwd
RUN git clone https://github.com/OrlandoSoto/github-wiki-search.git
RUN cd /usr/share/elasticsearch/github-wiki-search && git fetch --all
RUN cd /usr/share/elasticsearch/github-wiki-search && git checkout dockerize

RUN chown -R elasticsearch /usr/share/elasticsearch/github-wiki-search
RUN pip install -r /usr/share/elasticsearch/github-wiki-search/server/requirements.txt

