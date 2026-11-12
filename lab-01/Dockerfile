FROM python:3.12-slim AS build

WORKDIR /build
RUN python -m venv /opt/venv
COPY requirements.txt .
RUN /opt/venv/bin/python -m pip install --no-cache-dir -r requirements.txt

FROM python:3.12-slim

RUN useradd --create-home --uid 10001 app \
 && mkdir -p /data \
 && chown app:app /data

COPY --from=build /opt/venv /opt/venv

WORKDIR /app
COPY app.py .

ENV PATH="/opt/venv/bin:$PATH" \
    PORT=8080 \
    PYTHONUNBUFFERED=1

USER app
EXPOSE 8080
CMD ["python", "app.py"]