FROM python:3.11-alpine AS base

ARG GITHUB_ACTIONS
RUN if [ "$GITHUB_ACTIONS" != "true" ]; then \
        sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories; \
    fi

# timezone
RUN apk add -U tzdata

RUN apk add musl-dev gcc libxml2-dev libxslt-dev

FROM base AS dependencies

COPY ./requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt


FROM python:3.11-alpine AS release


COPY --from=dependencies /usr/local/bin /usr/local/bin
COPY --from=dependencies /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
# timezone
COPY --from=dependencies /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

WORKDIR /app


COPY . .

EXPOSE 5010

ENTRYPOINT [ "sh", "start.sh" ]
