FROM python:3.12-slim

WORKDIR /app

EXPOSE 5052

# Copy requirements.txt into the container
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

ADD . /app

# Add the sleep command to give MySQL time to start, then run migrate.py and app.py
ENTRYPOINT ["sh", "-c", "sleep 20 && python migrate.py && python app.py"]
