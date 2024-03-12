# Start from a Bun ready container
FROM oven/bun:latest
# Setup working folder
WORKDIR /opt/pipeline
COPY . .
# Install dependencies
RUN bun install
# Container's entrypoint command
ENTRYPOINT [ "bunx", "--bun", "js-runner", "ca-pipeline.ttl" ]