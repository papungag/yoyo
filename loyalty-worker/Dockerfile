FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip3 install --no-cache-dir -r requirements.txt

COPY . .

ENV HTTP_PORT='5002' JWT_SECRET='supersecret' REDIS_URL='redis://172.30.0.15:6379/0'

CMD [ "python3", "./run.py" ]