# Aragon App CMS

This repository stores dynamic data consumed by the [Aragon application](https://app.aragon.org).
It provides up-to-date information such as **featured DAOs** and **sanctioned addresses**.

## Featured DAOs

The list of featured DAOs is available at:
[**featured-daos.json**](https://raw.githubusercontent.com/aragon/app-cms/main/featured-daos.json)

### Data Structure

Each DAO entry is a JSON object with the following fields:

| Field            | Required | Description                        | Notes                                                                  |
| ---------------- | -------- | ---------------------------------- | ---------------------------------------------------------------------- |
| **name**         | ✅       | DAO name                           | —                                                                      |
| **description**  | ✅       | Brief description of the DAO       | —                                                                      |
| **logo**         | ✅       | URL to the DAO’s logo image        | —                                                                      |
| **network**      | ❌       | Network where the DAO is deployed  | Required if the network is supported by the Aragon application         |
| **networkLabel** | ❌       | Human-readable network name        | Required if the network is **not** supported by the Aragon application |
| **address**      | ❌       | On-chain DAO contract address      | Required if the DAO is supported by the Aragon application             |
| **ens**          | ❌       | ENS name of the DAO                | Required if the DAO is supported by the Aragon application             |
| **overrideUrl**  | ❌       | External link to the DAO’s website | Required if the DAO is **not** supported by the Aragon application     |

## Sanctioned Addresses

The list of sanctioned addresses is available at:
[**sanctioned-addresses.json**](https://raw.githubusercontent.com/aragon/app-cms/main/sanctioned-addresses.json)

This list is used to identify blockchain addresses that are restricted from accessing certain features of the Aragon application.
The list is derived from the official [OFAC Specially Designated Nationals (SDN) List](https://sanctionslist.ofac.treas.gov/Home/SdnList).

## DAO Overrides

DAO overrides allow hiding specific governance plugins for a given DAO without redeploying the application.

The configuration is available at:
[**dao-overrides.json**](https://raw.githubusercontent.com/aragon/app-cms/main/dao-overrides.json)

### Data Structure

The file is a JSON object where:

- the top-level key is the DAO identifier used by the app, for example `base-mainnet-0x...`
- the value is a DAO override object

Recommended schema:

```json
{
    "base-mainnet-0x123...": {
        "daoName": "Example DAO",
        "comment": "Explain why these plugins are hidden.",
        "pluginsToHide": [
            {
                "address": "0xabc...",
                "name": "Example Plugin",
                "comment": "Human-readable note about this exclusion."
            }
        ]
    }
}
```

| Field               | Required | Description                                                                 |
| ------------------- | -------- | --------------------------------------------------------------------------- |
| **daoName**         | ❌       | Human-readable DAO name for editors and reviewers                           |
| **comment**         | ❌       | High-level explanation of why the override exists                           |
| **pluginsToHide**   | ✅       | Array of hidden plugin objects                                              |
| **pluginsToHide.address** | ✅ | Plugin contract address used by the app to hide the plugin                  |
| **pluginsToHide.name** | ✅    | Human-readable plugin name                                                  |
| **pluginsToHide.comment** | ❌ | Per-plugin explanation or context                                           |

### Notes

1. `pluginsToHide` is the field used by the application logic.
2. Matching is done by `pluginsToHide[].address` and is case-insensitive.
3. `daoName`, `comment`, `pluginsToHide[].name`, and `pluginsToHide[].comment` are documentation metadata meant to keep the file understandable for humans.

## Feature Flags

Feature flags allow controlling feature visibility across different environments without code changes.

The feature flags configuration is available at:
[**feature-flags.json**](https://github.com/aragon/app-cms/blob/main/feature-flags.json)

### Data Structure

Feature flags can be configured in three formats:

#### 1. Simple format (same value for all environments)

```json
{
    "subDao": true
}
```

#### 2. Environment-specific format

```json
{
    "subDao": {
        "local": true,
        "preview": false,
        "development": false,
        "staging": false,
        "production": false
    }
}
```

#### 3. Mixed format

```json
{
    "debugPanel": true,
    "subDao": {
        "local": true,
        "preview": false,
        "production": false
    }
}
```

### Supported Environments

-   `local` - Local development
-   `preview` - Preview deployments
-   `development` - Development environment
-   `staging` - Staging environment
-   `production` - Production environment

### How It Works

1. Feature flags are first defined in code with default values
2. CMS overrides can modify these defaults per environment
3. Local cookie-based overrides (for debugging) take highest priority

**Priority order:**

```
Local override (cookie) > CMS override > Environment-specific (code) > Default (code)
```

### Adding a New Flag

1. The flag must first be defined in the codebase (`featureFlags.config.ts`)
2. The flag key must be added to the `FeatureFlagKey` type
3. Optionally, add the flag to this CMS file to override defaults

For more details, see the [Feature Flags README](https://github.com/aragon/app/src/shared/utils/featureFlags/README.md) in the application codebase.

## Spam Tokens

The list of spam tokens is available at:
[**spam-tokens.json**](https://raw.githubusercontent.com/aragon/app-cms/main/spam-tokens.json)

This list contains token contract addresses that are identified as spam or malicious. The Aragon application uses this list to filter out these tokens from being displayed in DAO treasuries and token lists.

### Data Structure

The file is a JSON object where keys are network identifiers and values are arrays of token contract addresses:

```json
{
    "ethereum-mainnet": [
        "0x2747eE1EE8490Ce2f1853600c28a3846353d9d31"
    ],
    "polygon-mainnet": [
        "0xcf68f02d7dD6a4642AE6a77f6A3676D0CBC834c9"
    ]
}
```

| Element                                | Type       | Description                                      |
| -------------------------------------- | ---------- | ------------------------------------------------ |
| **Top-level key (network identifier)** | `string`   | Network identifier (e.g., `ethereum-mainnet`)    |
| **Value**                              | `string[]` | Array of spam token contract addresses to filter |
