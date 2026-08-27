# MetaLend MCP

**Your co-pilot for stablecoin yield — from research all the way to execution.**

MetaLend is a remote MCP server that turns your AI agent into both a yield analyst
and a hands-on operator. Instead of manually comparing rates across lending
protocols and chains, MetaLend scans the market for you: it monitors the
best-paying pools for your specific stablecoins, highlights where you could earn a
higher APY, and lets you act on it — deposit, withdraw, or rebalance — without
leaving your agent.

No spreadsheets. No constant manual checking. No leaving money on the table.

---

## Non-custodial by design

MetaLend **never holds a private key and never signs anything itself.**

Every deposit, withdrawal, or config change is computed by the server and handed
back to you as a transaction to sign in your own wallet. The server then relays
your signed payload. You stay in full custody at every step.

---

## Install

Remote MCP server (Streamable HTTP):

```
https://mcp.metalend.tech/mcp
```

### Cursor

Add to `~/.cursor/mcp.json` (or a project `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "metalend": {
      "type": "http",
      "url": "https://mcp.metalend.tech/mcp"
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http metalend https://mcp.metalend.tech/mcp
```

### Claude Desktop / other clients

Point your client at the URL above using the HTTP (Streamable HTTP) transport.

---

## What you can do

- **Access live rates** — real-time yields across major protocols on multiple EVM chains
- **Track & alert** — monitor market shifts, compare current positions, surface a better yield
- **Monitor portfolios** — live balances, blended APY, and pending rewards for any public wallet address
- **Deposit & withdraw** — move stablecoins into the best pools or pull them back out
- **Rebalance & configure** — update which tokens and chains you track and your target allocation
- **Forecast actions** — look up transaction costs and minimum deposit amounts before committing

---

## Coverage

**Protocols:** Aave, Morpho, Euler

**Chains:** Multiple EVM chains, including Base, Ethereum, Polygon, Arbitrum, and Linea

---

## Tools

### Read-only discovery

| Tool | Purpose |
|---|---|
| `list_pools` | Live yields across protocols and chains |
| `get_balances` | Wallet balances and blended APY across every chain and pool |
| `get_bridge_balances` | Balances relevant to cross-chain moves |
| `get_rewards` | Unclaimed reward incentives across your pools |
| `get_config` | Your current rebalancer tracking preferences |
| `get_default_config` | Default rebalancer configuration |
| `get_token_info` | Token metadata and minimum deposit amounts |
| `get_transaction_costs` | Estimated gas / transaction costs per chain |
| `get_withdrawal_version` | Current withdrawal contract version |
| `get_deposit_status` / `get_withdrawal_status` | Status of a submitted deposit / withdrawal |

### Auth (wallet JWT)

| Tool | Purpose |
|---|---|
| `get_auth_challenge` | Get a SIWE challenge to sign |
| `submit_auth_verify` | Exchange the signed challenge for a wallet-scoped JWT |

### Write flows (`prepare_*` → sign → `submit_*`)

| Tool | Purpose |
|---|---|
| `prepare_deposit` / `submit_deposit` | Move stablecoins into a chosen pool |
| `prepare_withdrawal` / `submit_withdrawal` | Withdraw stablecoins from a pool |
| `prepare_config` / `submit_config` | Update rebalancer tokens, chains, and target allocation |

`prepare_*` computes everything and returns data for you to sign; it never signs.
`submit_*` relays a signature you produced yourself. The server holds no session
state — the wallet JWT from `get_auth_challenge` + `submit_auth_verify` is passed
explicitly on every `submit_*` call.

---

## Use cases

- Browse current stablecoin yields on Aave, Morpho, and Euler
- Compare rates across Base, Ethereum, Polygon, Arbitrum, and Linea
- Check a wallet's balances, blended APY, and pending rewards across every chain
- Deposit stablecoins into a chosen pool
- Withdraw stablecoins from a pool
- Move funds from a lower-yield pool into a higher-yield one
- Update rebalancer settings: which tokens and chains to track
- Set a target allocation so positions follow the best available yield
- Look up gas costs and minimum deposit amounts before moving funds
- Track unclaimed reward incentives across your pools
- Monitor a company treasury wallet across all chains in one view
- Get notified when a better yield becomes available

---

## Links

- Website: https://metalend.tech
- Transport: Streamable HTTP (remote MCP server)

---

## License

[MIT](./LICENSE)
