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
