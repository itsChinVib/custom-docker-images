FROM nvidia/cuda:12.1.1-devel-ubuntu22.04

RUN mkdir /softwares
WORKDIR /softwares

ENV DEBIAN_FRONTEND=noninteractive 
ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install pyenv
RUN apt-get update
RUN apt-get install -y --no-install-recommends curl software-properties-common ca-certificates build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
ENV HOME="/root"
WORKDIR ${HOME}
RUN apt-get install -y git
RUN git clone --depth=1 https://github.com/pyenv/pyenv.git .pyenv
ENV PYENV_ROOT="${HOME}/.pyenv"
ENV PATH="${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:${PATH}"
ENV PYTHON_VERSION=3.11.7
RUN pyenv install ${PYTHON_VERSION}
RUN pyenv global ${PYTHON_VERSION}

RUN apt-get update
RUN apt-get install -y curl wget gcc g++ libreoffice tesseract-ocr poppler-utils libmagic-dev pandoc ffmpeg

RUN mkdir /app
WORKDIR /app
COPY ./requirements.txt /app/requirements.txt

RUN pip install -r ./requirements.txt
RUN ls /usr/local/
ENV PATH="/usr/local/cuda/bin:/usr/local/cuda-12.1/bin:${PATH}"
ENV LD_LIBRARY_PATH="/usr/local/cuda/bin:/usr/local/cuda-12.1/lib64:${LD_LIBRARY_PATH}"
ENV LLAMA_CUBLAS=1
RUN CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python --upgrade --force-reinstall --no-cache-dir

RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get install git-lfs
RUN git lfs install


# Commands for downloading individual models
ENV MODEL_DIR /app/models
RUN mkdir -p $MODEL_DIR

RUN mkdir -p /app/scripts
RUN chmod -R +x /app/scripts

WORKDIR $MODEL_DIR

# WhereIsAI/UAE-Large-V1 embedding model
COPY ./scripts/download-uae-large-v1.sh /app/scripts/download-uae-large-v1.sh
RUN chmod -R +x /app/scripts
RUN /app/scripts/download-uae-large-v1.sh

# Mistral Instruct
COPY ./scripts/download-mistral-7b-instruct-0.1.sh /app/scripts/download-mistral-7b-instruct-0.1.sh
RUN chmod -R +x /app/scripts
RUN /app/scripts/download-mistral-7b-instruct-0.1.sh

WORKDIR /app
