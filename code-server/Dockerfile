FROM codercom/code-server:latest
# FROM linuxserver/code-server

USER root

# Base tools
RUN apt update && apt install -y \
    curl \
    git \
    build-essential \
    unzip \
    wget \
    software-properties-common

# -------------------------
# Java (Spring Boot ready)
# -------------------------
RUN apt install -y openjdk-17-jdk maven


# -------------------------
# Python (FIXED with venv)
# -------------------------
RUN apt install -y python3 python3-pip python3-venv python3-dev

# Create virtual environment
RUN python3 -m venv /opt/venv

# Activate venv path
ENV PATH="/opt/venv/bin:$PATH"

# Upgrade pip inside venv (NOW it works)
RUN pip install --upgrade pip

# Install dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# -------------------------
# Node.js + TypeScript
# -------------------------
# RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
#     && apt install -y nodejs

RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs

RUN npm install -g \
    typescript \
    ts-node \
    yarn
    
# -------------------------
# Cleanup
# -------------------------
RUN apt clean

# Fix permissions
RUN mkdir -p /home/coder/.local \
    && chown -R coder:coder /home/coder

USER coder