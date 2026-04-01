# Valet Provider Registry

Provider definitions for [Valet](https://github.com/peterday/valet) — encrypted API key management.

Each TOML file in `providers/` describes an API provider: setup URLs, environment variable names, key prefixes, validation endpoints, free tier details, and rotation characteristics.

## Usage

```bash
valet providers update          # clone/pull this registry
valet providers list            # list available providers
```

Providers are matched by environment variable name. When a required secret matches a known provider, `valet setup` opens the right browser page and validates the key format.

## Adding a provider

Create a TOML file in `providers/` following the existing examples. Required fields:

```toml
name = "my-provider"
display_name = "My Provider"
setup_url = "https://provider.com/api-keys"

[[env_vars]]
name = "MY_PROVIDER_API_KEY"
prefix = "mp_"
sensitive = true

[rotation]
strategy = "create-then-revoke"
```

## Custom registries

Teams can host their own provider registries:

```bash
valet providers add acme/internal-providers
```
