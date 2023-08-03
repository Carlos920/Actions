FROM python:3.9-alpine as builder

COPY requirements.txt .

RUN apk add --no-cache gcc g++ && \
    apk add --no-cache libjpeg-dev zlib1g-dev && \
        pip3 install --no-cache-dir Pillow && \
        pip3 install --no-cache-dir --upgrade pip && \
        pip3 install --no-cache-dir -r requirements.txt



FROM python:3.9-alpine

LABEL name="QQFlacMusicDownloader"

ENV TZ Asia/Shanghai

# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE=1

# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED=1

COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=builder /usr/local/lib/python3.9/site-packages /usr/local/lib/python3.9/site-packages

WORKDIR /workspace

COPY ./ /workspace

# RUN pip3 install --no-cache-dir --upgrade pip  -i https://mirrors.bfsu.edu.cn/pypi/web/simple && pip3 install --no-cache-dir -r /workspace/requirements.txt -i https://mirrors.bfsu.edu.cn/pypi/web/simple

# RUN apk add --no-cache gcc g++ && \
#         pip3 install --no-cache-dir --upgrade pip && \
#         pip3 install --no-cache-dir -r /workspace/requirements.txt && \
#         echo "==> Clean UP..."  && \
#         apk del gcc g++


EXPOSE 8899

CMD ["python3", "MainServer.py"]
