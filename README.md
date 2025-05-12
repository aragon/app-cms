# Aragon App CMS

## Featured DAOs

This repository contains the featured DAOs data used by Aragon applications.

#### Usage

The featured DAOs data can be accessed at:
https://raw.githubusercontent.com/aragon/app-cms/main/featured-daos.json

#### Data Format

Each DAO object contains the following fields:

| Field            | Required | Description                 | Notes                                                      |
| ---------------- | -------- | --------------------------- | ---------------------------------------------------------- |
| **name**         | `true`   | Name of the DAO.            | -                                                          |
| **description**  | `true`   | Description of the DAO.     | -                                                          |
| **logo**         | `true`   | URL of the logo of the DAO. | -                                                          |
| **network**      | `false`  | Network of the DAO          | Required if the network is supported by the Aragon App     |
| **networkLabel** | `false`  | Label of the DAO network    | Required if the network is not supported by the Aragon App |
| **address**      | `false`  | Address of the DAO          | Required if the DAO is supported by the Aragon App         |
| **ens**          | `false`  | ENS of the DAO              | Required if the DAO is supported by the Aragon App         |
| **overrideUrl**  | `false`  | External URL of the DAO     | Required if the DAO is not supported by the Aragon App     |
