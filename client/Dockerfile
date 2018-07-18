FROM node:9 as builder

ADD . /app

WORKDIR /app

RUN apt-get -y update 
RUN apt-get -y upgrade
RUN apt-get -y install git-all
RUN apt-get -y install -y procps

RUN yarn install
RUN ./node_modules/.bin/grunt vendor
RUN ./node_modules/.bin/grunt
RUN ./node_modules/.bin/grunt dist

FROM nginx

WORKDIR /usr/share/nginx/html/

COPY --from=builder /app/dist/ .
COPY nginx/default.conf /etc/nginx/conf.d/

CMD ["nginx", "-g", "daemon off;"]
