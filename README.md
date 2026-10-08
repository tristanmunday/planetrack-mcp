# PlaneTrack MCP server

Flight data for Claude, ChatGPT and any MCP client: aircraft airborne near a point, a single aircraft's track, past legs of a flight number, on-time reliability for a flight, route or airport (US airspace), and what flew over an address.

Remote server (Streamable HTTP): `https://planetrack.ai/api/analysis/mcp`
Auth: header `X-API-Key: <your key>`. A free key (2,000 credits a month) takes a minute at https://planetrack.ai/dashboard.html. Credits per call are listed at https://planetrack.ai/docs.html#mcp.

## Tools

| Tool | What it returns | Credits |
| --- | --- | --- |
| live_aircraft_near | Aircraft currently airborne within radius_km of a latitude/longitude, nearest first | 10 |
| aircraft_track | Positions of one aircraft (Mode-S hex) over the last 5 to 1440 minutes | 20 |
| flight_history | Past legs of a flight number as flown: dates, airports, times, aircraft | 20 |
| flight_reliability | On-time performance for a flight number, route or departure airport over 7 to 90 days (US) | 20 |
| overhead_summary | How many aircraft passed within km of a point over the last 1 to 3 days, lowest pass, busiest hour, night passes | 20 |

## Claude Desktop

```json
{
  "mcpServers": {
    "planetrack": {
      "url": "https://planetrack.ai/api/analysis/mcp",
      "headers": {"X-API-Key": "pt_live_..."}
    }
  }
}
```

## Quick test

```bash
curl -s https://planetrack.ai/api/analysis/mcp -H "X-API-Key: pt_live_..." -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Data: the FAA's SWIM flight records (US) plus PlaneTrack's own ADS-B receiver network and community aggregators. Aircraft on the FAA's LADD privacy list are excluded. Terms: https://planetrack.ai/terms.html
