# Start from a Bun ready container
FROM oven/bun:latest
# Install java 17 (to run the RML and XQuery engines)
RUN apt-get update
RUN apt-get install -y openjdk-17-jre-headless
# Install wget
RUN apt-get install -y wget
# Setup working folder
WORKDIR /opt/pipeline
COPY . .
# Install dependencies
RUN bun install
# Hack to get around bun's issue of not running preinstall scripts (in this case on prefix-ns)
RUN cd node_modules/prefix-ns && rm data.json && bun preinstall.js
# Expose input HTTP port
EXPOSE 3333
# Container's entrypoint command
ENTRYPOINT [ "bunx", "--bun", "@rdfc/js-runner" ]