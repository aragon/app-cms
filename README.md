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
