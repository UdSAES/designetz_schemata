# Schemata for Data Exchange Between Services
In this repository, the formats for exchanging data _between services_ within Designetz are defined. Mock-up data and guidelines on using this repository are given in addition to the actual schemata definitions, which are defined according to the [OpenAPI specification (OAS)](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md).

![](https://github.com/UdSAES/designetz_schemata/blob/master/resources/logos_uds_aes_designetz_bmwi.png)

__You currently checked out the branch `dev`, which is used for working on new releases. Schemata that only exist on this branch are not stable yet!.__

## Why this Repository?
The specification of the format and content of messages exchanged when interacting with a service constitute an important part of the service description. In order to avoid duplicate work, ensure consistency/interoperability and follow the evolution of the respective specifications with confidence, the possibility to split an OpenAPI-description across several files shall be leveraged.

Each partner that develops a service can use the schemata provided in this repository as part of the service interface description by referencing them. Mock-up data can be provided for others and/or mock-up data provided by others can be used for testing.

All files in this repository are versioned using [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html) (semver), therefore the degree of compatibility between versions is unambiguously defined by the version number. All files on the master-branch are safe to use; files that only exist on other branches are not!

## How to Use a Schema for Developing a Service
Instead of copy-pasting the schema for a certain message into the description of a service, every partner that wishes to use a schema shall _reference_ it as shown below.
```json
{
  "swagger": "2.0",
  "info": {},
  "paths": {
    "/resource": {
      "get": {
        "summary": "...",
        "responses": {
          "200": {
            "description": "The result in the externally defined format.",
            "schema": {
              "$ref": "#/definitions/Result"
            }
          }
        }
      }
    }
  },
  "definitions": {
    "Result": {
      "$ref": "https://raw.githubusercontent.com/UdSAES/designetz_schemata/master/schemata/forecast/schema_v0.2.1-oas2.json#/Result"
    }
  }
}

```
The link to the specification is obtained by clicking the "Raw"-button on GitHub. Bear in mind that this link can either represent a [schema file](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#relative-schema-file-example) or a [file with embedded schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#relative-files-with-embedded-schema-example) (the latter shown above).

## How to Contribute to the Schema Definitions
Several measures for ensuring that this repository can become a reliable and robust resource for schemata are suggested. They are based on the [development guidelines](https://github.com/OAI/OpenAPI-Specification/blob/master/DEVELOPMENT.md) for the OAS and outlined below.

### Structure and Content of the Repository
Each schema "lives" in a subdirectory of `schemata/`. Inside this directory, there MUST exist at least one version of the schema named `schema_vX.Y.Z-oasN.json` where `X.Y.Z` represent the version number and `N` is either `2` or `3`, depending on the version of the OAS used. Additionally, there SHOULD exist a subdirectory `./mock-up_data/` holding examples of messages that match the respective schema. Each example MUST indicate the version(s) it refers to, for example `global_irradiance_v0.2.x.json`. If possible, the schema should be explained comprehensively directly within the OAS/.json-file. A separate `README.md` may be used to provide additional information, such as a revision history.

### Branches
There are four persistent branches:
```
master     // the released versions of the schemata
dev        // the branch to be used for working on additions/changes
```
Changes to the schemata are integrated into the `dev`-branch. When a new version shall be released, it will be merged into the master branch by the maintainer of the repository using a pull request. It is not possible to push commits to the master branch directly.

### Contributing Using Issues and Pull Requests
If you want to discuss something, open an issue on GitHub. If you want to discuss something _and_ provide a solution, do the following:
1. Check out the `dev`-branch, and then create a new branch for your changes.
2. Implement a first suggestion of your changes.
3. Open a pull request from your branch into the development branch.

## Further Information
* All files in this repository are placed under the MIT license.
* __Please do not hesitate to get in touch!__
