FROM node:9-alpine as builder

ARG es_end_point=http://elasticsearch:9200/
ENV ES_END_POINT $es_end_point

ADD . /app

WORKDIR /app

RUN apk update
RUN apk upgrade
RUN apk add git

RUN yarn install
RUN ./node_modules/.bin/grunt vendor
RUN ./node_modules/.bin/grunt
RUN ./node_modules/.bin/grunt dist

RUN yarn global add mustache

COPY nginx/default.conf /app
RUN echo "{\"ES_END_POINT\": \"$ES_END_POINT\"}" | \
    mustache - /app/default.conf > \
    /app/default.conf-new

FROM nginx

WORKDIR /usr/share/nginx/html/

COPY --from=builder /app/dist/ .

COPY --from=builder /app/default.conf-new /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]
