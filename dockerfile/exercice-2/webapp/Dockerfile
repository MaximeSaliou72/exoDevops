FROM python:3.9

WORKDIR /app

COPY requirements.txt /app/
COPY server.py /app/

RUN pip install --no-cache-dir -r requirements.txt

CMD [ "python", "server.py" ]

EXPOSE 5000
