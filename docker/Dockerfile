FROM nvidia/cuda:13.5.0-cudnn-runtime-ubuntu24.04@sha256:0490edd1b0d88388497dfbe3762d0deab0ded3baf4828616636c17cbd44723e3
RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends passwd python3.12-venv \
    && rm -rf /var/lib/apt/lists/*
RUN python3.12 -m venv /opt/venv \
    && /opt/venv/bin/python -m pip install --upgrade pip \
    && /opt/venv/bin/python -m pip install --no-cache-dir faster-whisper \
    && useradd --create-home --uid 10001 app
ENV PATH="/opt/venv/bin:${PATH}"
WORKDIR /app
COPY --chown=10001:10001 infer.py jfk.flac ./
USER 10001:10001
CMD ["python", "infer.py"]
