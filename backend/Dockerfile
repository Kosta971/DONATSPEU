FROM python:3.10

WORKDIR /app
COPY . /app

RUN pip install fastapi uvicorn sqlalchemy aiosqlite python-multipart passlib[bcrypt] jose

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
