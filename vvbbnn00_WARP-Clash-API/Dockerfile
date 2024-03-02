FROM python:3.11-alpine AS builder-image

WORKDIR /app

# Install dependencies for building some Python packages
# Check if in Github Actions, if not, change Alpine source to Aliyun
ARG GITHUB_ACTIONS
RUN if [ "$GITHUB_ACTIONS" != "true" ]; then \
        sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories; \
    fi
RUN apk add --no-cache bash build-base libffi-dev openssl-dev \
    && rm -rf /var/cache/apk/*

# Install Python dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt 

FROM python:3.11-alpine AS release 

LABEL name="WARP-Clash-API"

COPY --from=builder-image /usr/local/bin /usr/local/bin
COPY --from=builder-image /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages

RUN apk add --no-cache bash \
    && rm -rf /var/cache/apk/*

WORKDIR /app

# Copy the rest of the code
COPY . .
RUN chmod +x ./scripts/*.sh

ENV TZ Asia/Shanghai

# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE=1
# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED=1

# Set environment variables
ENV RUN_IN_DOCKER=true

CMD ["/bin/sh", "./scripts/run.sh"]
