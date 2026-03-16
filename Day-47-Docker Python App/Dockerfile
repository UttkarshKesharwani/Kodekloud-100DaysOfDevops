



FROM python:3.12-alpine

WORKDIR /app

COPY src/requirements.txt .

RUN pip install -r requirements.txt

COPY src/ .

EXPOSE 5002

CMD ["python","server.py"]
