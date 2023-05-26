# allstar-jsonschema
A JSON schema to configure [allstar](https://github.com/ossf/allstar) which is a GitHub App to set and enforce security policies

We can use this schema to validate the configuration file for allstar in IDEs like VSCode and JetBrain.

- [allstar.json](./allstar.json): Org-level config
- [branch_protection.json](./branch_protection.json): a schema for `branch_protection.yml`
- [binary_artifacts.json](./binary_artifacts.json): a schema for `binary_artifacts.yml`
- [dengerous_workflow.json](./dengerous_workflow.json): a schema for `dengerous_workflow.yml`
- [outside.json](./outside.json): a schema for `outside.yml`
- [scorecard.json](./scorecard.json): a schema for `scorecard.yml`
- [security.json](./security.json): a schema for `security.yml`
- [admin.json](./admin.json): a schema for `admin.yml`
- [actions.json](./actions.json): a schema for `actions.yml`

## NOTE
The JSON schema file was manually created from the struct type in golang.

- https://github.com/ossf/allstar/blob/main/pkg/config/config.go#L33-L67
