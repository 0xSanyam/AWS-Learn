# Use an official Ubuntu-based dev container
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04


RUN curl -s "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip -q awscliv2.zip \
    && sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli \
    && rm -rf awscliv2.zip aws

# Set environment variables (like Gitpod's 'env')
ENV AWS_CLI_AUTO_PROMPT=on-partial

# Optional: Add other tools (Terraform, CDK, etc.)
# RUN apt-get update && apt-get install -y terraform

# Set the working directory (like Gitpod's workspace)
WORKDIR /workspaces