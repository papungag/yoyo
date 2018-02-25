FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip3 install --no-cache-dir -r requirements.txt

COPY . .

ENV HTTP_PORT='5000' JWT_SECRET='supersecret'

CMD [ "python3", "./run.py" ]