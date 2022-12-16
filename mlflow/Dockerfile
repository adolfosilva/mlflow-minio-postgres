FROM python:3.10-slim AS build
RUN apt-get update && apt-get install -y build-essential libpq-dev
COPY requirements.txt .
RUN pip install --user -r requirements.txt

FROM python:3.10-slim
EXPOSE 5000
RUN apt-get update && apt-get install -y libpq-dev
COPY --from=build /root/.local /root/.local
ENV PATH=/root/.local/bin:$PATH
CMD AWS_ACCESS_KEY_ID=$MINIO_ACCESS_KEY AWS_SECRET_ACCESS_KEY=$MINIO_SECRET_KEY mlflow server --host 0.0.0.0 --port 5000
