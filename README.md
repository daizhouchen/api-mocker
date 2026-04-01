# api-mocker

> Give me an API spec, get a running mock server in seconds.

An [OpenClaw](https://openclawskill.ai) skill that generates a fully functional Express.js mock API server from OpenAPI/Swagger specs or verbal descriptions, complete with smart fake data and CRUD operations.

## Features

- **OpenAPI 3.0 Parsing** — Full `$ref` resolution, `allOf`/`oneOf` merging
- **Smart Fake Data** — Field-name inference (name→person, email→email, price→dollars)
- **Referential Integrity** — Foreign keys reference actual records (e.g., `user_id` in orders matches real users)
- **Full CRUD** — GET (list + single), POST, PUT, DELETE with in-memory store
- **Pagination** — `?page=1&limit=10` on all list endpoints
- **CORS Enabled** — Ready for frontend development
- **Configurable Delay** — Simulate network latency with `DELAY_MS` env var

## Installation

```bash
npx @anthropic-ai/claw@latest skill add daizhouchen/api-mocker
```

## How It Works

1. **Parse** — `scripts/parse_openapi.py` extracts routes from OpenAPI YAML/JSON
2. **Generate Data** — `scripts/fake_data.py` creates realistic, referentially consistent data
3. **Generate Server** — `scripts/generate_server.js` produces a complete Express project
4. **Run** — `npm install && node server.js`

## Manual Usage

```bash
# Parse an OpenAPI spec
python3 scripts/parse_openapi.py path/to/openapi.yaml

# Generate fake data
python3 scripts/fake_data.py

# Generate the Express server
node scripts/generate_server.js

# Start the mock server
cd mock-server && npm install && node server.js
# Server running at http://localhost:3456
```

## Trigger Phrases

- "mock api" / "mock server"
- "后端还没好我需要先开发前端"
- "假接口" / "前端联调" / "模拟后端"

## Project Structure

```
api-mocker/
├── SKILL.md                    # Skill definition and workflow
├── scripts/
│   ├── parse_openapi.py        # OpenAPI spec parser
│   ├── fake_data.py            # Smart fake data generator
│   └── generate_server.js      # Express server code generator
├── assets/
│   └── sample-ecommerce.yaml   # Sample e-commerce OpenAPI spec
└── README.md
```

## Generated Server Structure

```
mock-server/
├── server.js          # Main server file (port 3456)
├── routes/            # One file per resource
├── data/              # JSON data files
├── package.json       # Express dependency
└── README.md          # Endpoint documentation
```

## Requirements

- Python 3.8+ (for spec parsing and data generation)
- Node.js 16+ (for the generated mock server)
- PyYAML (`pip install pyyaml`)

## Limitations

- In-memory data store (resets on restart — by design for mock usage)
- Default port 3456 (configurable in generated server.js)

## License

MIT
