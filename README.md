# Anchor Vault

A Solana program built with the Anchor framework that implements a personal SOL vault. Users can initialize a vault, deposit and withdraw SOL, and close the vault to reclaim all funds including rent.

## Program Overview

The program exposes four instructions:

- **Initialize** -- Creates a vault state PDA and a vault PDA for the signer. Transfers the minimum rent-exempt balance into the vault.
- **Deposit** -- Transfers a specified amount of SOL from the user into the vault.
- **Withdraw** -- Transfers a specified amount of SOL from the vault back to the user via a PDA-signed CPI.
- **Close** -- Drains all remaining SOL from the vault to the user and closes the vault state account, refunding its rent.

## Architecture

```
programs/anchor-vault-q1-26/src/lib.rs   -- Program logic (instructions + accounts)
tests/anchor-vault-q1-26.ts             -- Integration tests
```

### Accounts

| Account      | Type            | Description                                      |
|--------------|-----------------|--------------------------------------------------|
| `VaultState` | PDA (`state`)   | Stores the vault and state bump seeds             |
| `Vault`      | PDA (`vault`)   | System account that holds the deposited SOL       |

### PDA Seeds

- **VaultState**: `["state", user_pubkey]`
- **Vault**: `["vault", vault_state_pubkey]`

## Prerequisites

- Rust and Cargo
- Solana CLI
- Anchor CLI (v0.32+)
- Node.js and Yarn

## Build

```bash
anchor build
```

## Test

```bash
anchor test
```
## Tests Passing
![Test Passing](<public/Screenshot 2026-02-07 114121.png>)

The test suite covers the full lifecycle: initialize, deposit, withdraw, and close. It verifies PDA derivation, balance changes, and account cleanup.

## Program ID

```
AcoYk1Abw2keL4CpHFFN9PCUEBDzkc268QXBFVi9nkDZ
```