FROM python:3.11-alpine

LABEL name="QQFlacMusicDownloader"

ENV TZ Asia/Shanghai

# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE=1

# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED=1

WORKDIR /workspace

ADD ./ /workspace

# RUN pip3 install --no-cache-dir --upgrade pip  -i https://mirrors.bfsu.edu.cn/pypi/web/simple && pip3 install --no-cache-dir -r /workspace/requirements.txt -i https://mirrors.bfsu.edu.cn/pypi/web/simple

RUN apk add --no-cache gcc g++ && \
        pip3 install --no-cache-dir --upgrade pip && \
        pip3 install --no-cache-dir -r /workspace/requirements.txt && \
        echo "==> Clean UP..."  && \
        apk del python3-pip gcc g++ && \
        apk cache clean

EXPOSE 8899

CMD ["python3", "MainServer.py"]