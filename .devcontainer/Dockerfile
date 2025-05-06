FROM mcr.microsoft.com/devcontainers/python:3.12

# Install system dependencies for data science packages like GeoPandas
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        libspatialindex-dev \
        gdal-bin \
        libgdal-dev \
        libproj-dev \
        proj-bin \
        python3-rtree \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

# Install Python linting/formatting tools
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir pylint autopep8 black yapf flake8 mypy pycodestyle pydocstyle bandit

# Setup permissions for the vscode user
RUN mkdir -p /home/vscode/.vscode-server/extensions \
    && chown -R vscode:vscode /home/vscode/.vscode-server

# Set up a virtual environment path that will be used later
ENV VIRTUAL_ENV=/workspaces/DataDemo/.venv

# Setup so Python packages are installed inside the project directory
ENV PYTHONPATH=/workspaces/DataDemo

# Change to non-root user
USER vscode