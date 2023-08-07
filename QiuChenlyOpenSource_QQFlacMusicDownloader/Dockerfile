FROM python:3.11-alpine AS base

RUN apk add --no-cache gcc g++ jpeg-dev zlib-dev \
    && rm -rf /var/cache/apk/*


FROM base AS dependencies

WORKDIR /workspace
COPY requirements.txt .

RUN pip3 install --no-cache-dir --upgrade pip -i https://mirrors.bfsu.edu.cn/pypi/web/simple && \
    pip3 install --no-cache-dir -r requirements.txt -i https://mirrors.bfsu.edu.cn/pypi/web/simple


FROM dependencies AS source 

WORKDIR /workspace
COPY ./ .


FROM source AS release 

LABEL name="QQFlacMusicDownloader"

ENV TZ Asia/Shanghai
# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE=1
# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED=1

EXPOSE 8899

CMD ["python3", "MainServer.py"]
