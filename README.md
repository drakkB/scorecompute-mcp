# ScoreCompute MCP

Remote [MCP](https://modelcontextprotocol.io) server that gives AI assistants 38 tools for bounded scientific calculation, including 22 engines written in Rust. Results come with their assumptions and limits, and depend on the inputs and model you supply.

**Hosted endpoint (no install, no API key for bounded public access):**

```
https://scorecompute.com/mcp
```

Transport: Streamable HTTP. Website: [scorecompute.com](https://scorecompute.com/). This repository holds documentation and examples; the engines run on the hosted service and their source is not published here.

## Connect

Claude Desktop, Claude Code, Cursor and other clients that read `mcpServers`:

```json
{
  "mcpServers": {
    "scorecompute": {
      "type": "http",
      "url": "https://scorecompute.com/mcp"
    }
  }
}
```

To expose only some tools, add 1 to 8 names: `https://scorecompute.com/mcp?tools=propagate_uncertainty,audit_statistics`. This reduces the catalogue the assistant loads; it is not an authorization boundary. Client-by-client steps: [scorecompute.com/connect](https://scorecompute.com/connect/).

## What it can calculate

| Question | Tool | Guide or demo |
|---|---|---|
| How do I propagate measurement uncertainty, with units? | `propagate_uncertainty` | [Guide](https://scorecompute.com/guides/uncertainty-propagation/) |
| Can this rounded mean come from integer data? | `audit_statistics` | [Guide](https://scorecompute.com/guides/grim-grimmer/) |
| Does this numerical claim hold, with a signed receipt? | `verify_claim` | [Verify](https://scorecompute.com/verify/) |
| Can this tour meet a deadline? | `route_optimizer`, `simulate_plan` | [Mission](https://scorecompute.com/missions/robust-route/) |
| Where is this body in an ideal two-body orbit? | `compute_orbit` | [Demo](https://scorecompute.com/demos/compute-orbit/) |
| What are the vibration modes of this polygon? | `hear_the_shape` | [Demo](https://scorecompute.com/demos/hear-the-shape/) |

All tools: [engine library](https://scorecompute.com/engines/), [llms.txt](https://scorecompute.com/llms.txt). Your client's `tools/list` gives the current schemas and limits.

## Recorded example

[`examples/uncertainty-nonlinear.json`](examples/uncertainty-nonlinear.json) is one public call to `propagate_uncertainty`, recorded on 2 November 2026 on release 0.17.1, with its full arguments and response.

Model `x1 * x2`, two independent normal inputs with value 1 and standard uncertainty 1:

| Method | Standard uncertainty | 95% interval |
|---|---:|---:|
| First-order GUM | 1.414 | [-1.77, 3.77] |
| Monte Carlo (200,000 draws, seed 7) | 1.732 | [-1.74, 5.29] |

The tool returns `linearization_inadequate` and recommends the Monte Carlo result. The exact standard deviation for this model is about 1.732.

## Limits

- A result is conditional on the supplied inputs and model. It is not a certification or a regulatory approval.
- Evidence cards cover the listed test cases, not every input: [scorecompute.com/trust](https://scorecompute.com/trust/).
- Availability is observed, not guaranteed: [scorecompute.com/status](https://scorecompute.com/status/).
- Public access is rate limited. Plans: [scorecompute.com/pricing](https://scorecompute.com/pricing/).

## Contact

[contact@scorezenith.com](mailto:contact@scorezenith.com). ScoreCompute is part of the [ScoreZenith](https://scorezenith.com/) ecosystem.
