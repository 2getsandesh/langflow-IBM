# Langflow Observability with Traceloop Integration Guide

This guide explains how to integrate Traceloop and Instana observability platforms with your Langflow applications to monitor and analyze LLM performance.

## About Traceloop

Traceloop is an observability platform designed for LLM (Large Language Model) applications. It provides developers with detailed insights into how LLMs behave in real-world flows, offering powerful tools like trace visualizations, token usage, latencies, and prompt/response inspection.

## Prerequisites

Before setting up observability, ensure you have:
- A Traceloop API key (for Traceloop integration)
- An Instana endpoint and key (for Instana integration)
- A running Langflow application setup

## Integration Options

### Option 1: Connect Langflow to Traceloop

#### Step 1: Obtain Your Traceloop API Key
1. Navigate to the [Traceloop API Key settings](https://app.traceloop.com/settings/api-keys) to generate  your API keys.

2. Generate or copy your Traceloop API key

#### Step 2: Configure Environment Variables
1. Create a `.env` file in the root directory of your Langflow application (if it doesn't exist already)
2. Add your Traceloop API key to the `.env` file:
   ```
   TRACELOOP_API_KEY=<your_traceloop_api_key>
   ```
3. Save the `.env` file

#### Step 3: Start Langflow with Environment Variables
Launch your Langflow application using the environment file:
```bash
uv run langflow run --env-file .env
```

Once configured, Traceloop will automatically begin monitoring and collecting telemetry data from your LLM applications.

### Option 2: Connect Langflow to Instana

#### Step 1: Configure Environment Variables
1. Create a `.env` file in the root directory of your Langflow application (if it doesn't exist already)
2. Add the following configuration to the `.env` file:
   ```
   OTEL_EXPORTER_OTLP_ENDPOINT="<instana_endpoint>"
   OTEL_EXPORTER_OTLP_HEADERS="x-instana-key=<instana-agent-key>"
   OTEL_SERVICE_NAME="<service-name>"
   ```
3. Save the `.env` file

#### Step 2: Start Langflow with Environment Variables
Launch your Langflow application using the environment file:
```bash
uv run langflow run --env-file .env
```

## Testing Your Integration

To verify that observability is working correctly:

1. **Run a flow in Langflow:**
   - In Langflow, select the "Simple Agent" starter project
   - In the **Agent** component's **API Key** field, enter your LLM API key
   - Click **Playground**
   - Ask your Agent several questions to generate test traffic

2. **View Traces:**
   - **For Traceloop:** Visit [Traceloop traces dashboard](https://app.traceloop.com/) to view your traces
   - **For Instana:** Search for "langflow" in the "Services" section of your Instana dashboard

## Troubleshooting

If you don't see traces appearing:
- Verify that your API keys and endpoints are correct in the `.env` file
- Ensure the `.env` file is in the correct root directory
- Confirm that Langflow is starting with the `--env-file .env` parameter
- Check that you've generated sufficient test traffic through the Playground


For additional configuration options and advanced features, refer to the respective platform documentation for Traceloop or Instana.