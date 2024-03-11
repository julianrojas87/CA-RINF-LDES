# Start from a Bun ready container
FROM oven/bun:latest
# Setup working folder
WORKDIR /opt/pipeline
COPY . .
# Install dependencies
RUN bun install
# Expose input HTTP port
EXPOSE 3333
# Container's entrypoint command
ENTRYPOINT [ "bunx", "--bun", "js-runner" ]