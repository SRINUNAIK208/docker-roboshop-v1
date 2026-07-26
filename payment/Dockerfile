FROM python:3.11-alpine AS builder 
WORKDIR /app 
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip3 install --no-cache --prefix=/install -r requirements.txt 


FROM python:3.11-alpine 
WORKDIR /app 
RUN apk add --no-cache pcre-dev
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /install /usr/local
COPY *.py /app
COPY payment.ini /app
USER roboshop
CMD ["uwsgi","--ini","payment.ini"]

 