# Use a smaller base image
FROM python:3.12-alpine

# Install necessary dependencies
RUN apk update && apk add --no-cache \
    bash \
    git \
    chromium \
    chromium-chromedriver \
    wget \
    curl \
    ca-certificates \
    && rm -rf /var/cache/apk/*

# Install Python packages
RUN pip install --no-cache-dir selenium requests

# Add a non-root user for Codespaces
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN addgroup -g $USER_GID $USERNAME \
    && adduser -D -s /bin/bash -u $USER_UID -G $USERNAME $USERNAME

USER $USERNAME

# Set Chrome options for Selenium
ENV CHROME_BIN=/usr/bin/chromium-browser \
    CHROME_DRIVER=/usr/bin/chromedriver

# Create a working directory
WORKDIR /home/$USERNAME/app

# Clone the repository and initialize submodules
RUN git clone --recurse-submodules https://github.com/lokswin/literate-fiesta . \
    && git submodule update --init --recursive

# Optional: Copy the script to the working directory
# COPY external_repo/your_script.py .

# CMD to run your script
# CMD ["python", "external_repo/your_script.py"]
