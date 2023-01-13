# buildkite-plugin-foreach

A plugin for reducing duplication in buildkite pipelines.
After producing the pipeline, a `buildkite-agent pipeline upload` will be performed to ship the generated pipeline.

## Example
Add the following to your `pipeline.yml`:

```yml
steps:
  - plugins:
    - dizzzan/foreach#v1.0.0:
        steps: my-steps.yml
        key: env
        foreach:
          - qa
          - stage
          - prod
        wait_between: true
```

## Configuration

### `steps` (Required, string)
The path to a file which will be used as the template. 
This should be just the steps themselves, without the `steps:` mapping.
```yml
- label: Step for {key}
  command: "step.sh --input {key}

```

### `foreach` (Required, array of string)
The list of values to iterate over.

###  `key` (string, default='key')
The key which will be passed as the current value of the `foreach` array. Your pipeline definition will replace `{key}` with the value of each iteration.

### `wait_between` (boolean, default=false)