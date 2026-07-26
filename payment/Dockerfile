FROM python:3.11-alpine AS builder 
WORKDIR /app 
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip3 install --no-cache --prefix=/install -r requirements.txt 


FROM python:3.11-alpine 
WORKDIR /app 
RUN apk add --no-cache pcre-dev
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

COPY --from=builder /install /usr/local
COPY --chown=roboshop:roboshop *.py /app
COPY --chown=roboshop:roboshop payment.ini /app
USER roboshop
CMD ["uwsgi","--ini","payment.ini"]

 