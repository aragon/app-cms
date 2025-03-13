# Aragon App CMS

## Featured DAOs

This repository contains the featured DAOs data used by Aragon applications.

#### Usage

The featured DAOs data can be accessed at:
https://raw.githubusercontent.com/aragon/app-cms/main/featured-daos.json

#### Data Format

Each DAO object contains the following fields:

| Field            | Description                                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------------- |
| **name**         | Name of the DAO.                                                                                              |
| **description**  | Description of the DAO.                                                                                       |
| **logo**         | URL of the logo of the DAO.                                                                                   |
| **network**      | Network the DAO is deployed on (optional and should only be added if the network is supported by Aragon app). |
| **networkLabel** | Network label, should be provided if the network is not supported in the Aragon app.                          |
| **address**      | The address of the DAO (this is optional and can be omitted for DAOs deployed outside of the aragon app).     |
| **overrideUrl**  | Used if we want to link to an external page.                                                                  |
