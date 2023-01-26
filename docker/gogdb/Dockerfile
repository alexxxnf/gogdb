# syntax=docker/dockerfile:experimental
FROM python:3.11-alpine3.17 as builder

ENV POETRY_VIRTUALENVS_CREATE=false

RUN --mount=type=cache,target=/root/.cache/pip,sharing=locked,id=pip-cache \
    pip3 install --cache-dir /root/.cache/pip --progress-bar off poetry

# These packages are needed for some Python packages to build their binaries
RUN --mount=type=cache,target=/root/.cache/apk,sharing=locked,id=apk-cache \
    apk add --cache-dir /root/.cache/apk \
        gcc \
        libffi-dev \
        musl-dev \
        python3-dev

WORKDIR /app

COPY poetry.lock pyproject.toml /app/

RUN --mount=type=cache,target=/root/.cache/pip,sharing=locked,id=pip-cache \
    mkdir /dependencies \
        && poetry export -o /dependencies/requirements.txt \
        && pip3 wheel \
            --cache-dir /root/.cache/pip \
            --wheel-dir /dependencies \
            --progress-bar off \
            -r /dependencies/requirements.txt

COPY . /app/

RUN poetry build -f wheel \
    && mv dist/* /dependencies


FROM python:3.11-alpine3.17

ENV PYTHONUNBUFFERED=y

RUN --mount=type=bind,from=builder,source=/dependencies,target=/dependencies \
    addgroup --system --gid 101 gogdb \
    && adduser --system --disabled-password --ingroup gogdb --no-create-home --home /nonexistent --gecos "GOG DB" --shell /bin/false --uid 101 gogdb \
    && pip3 install --no-cache-dir --no-index -f /dependencies gogdb

USER gogdb

EXPOSE 3031

CMD ["hypercorn", \
        "--bind", "0.0.0.0:3031", \
        "gogdb.application:app" \
    ]
