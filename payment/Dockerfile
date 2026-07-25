FROM python:3.11-alpine as builder 
WORKDIR /app 
COPY requirements.txt .
RUN pip3 install --prefix=/install -r requirements.txt 
COPY *.py . 
COPY payment.ini .

FROM python:3.11-alpine 
WORKDIR /app 
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder /install /usr/local
COPY --from=builder /app .
USER roboshop
CMD ["uwsgi","--ini","payment.ini"]

 