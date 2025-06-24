FROM python:3.12-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN python -m venv /env && /env/bin/pip install -r requirements.txt
COPY app.py .



FROM python:3.12-alpine
WORKDIR /app
COPY --from=builder /app /app
COPY --from=builder /env /env
ENV PATH="/env/bin:$PATH"
ENTRYPOINT ["python", "app.py"]
