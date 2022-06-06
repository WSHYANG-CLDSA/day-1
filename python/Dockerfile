ARG VER=latest
FROM python:${VER}

WORKDIR /usr/src/app

RUN apt-get update && apt-get install curl

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY public public
COPY templates templates
COPY *.py ./
COPY run.sh .

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 CMD curl -s localhost:3000/healthz || exit 1

EXPOSE 3000
ENV INSTANCE_NAME="my app"
ENV INSTANCE_HASH="DEADBEEF"

ENTRYPOINT [ "/usr/src/app/run.sh" ]