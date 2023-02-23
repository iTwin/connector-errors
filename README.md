# connector-errors

This repository serves as an authority for errors that a Connector can generate.

## fatal-errors.json

This file lists all possible errors found in generated SyncError.json files when a Connector terminates abnormally.
A "fatal error" means that the Connector was unable to run to completion (i.e. a clear and obvious problem).

### Rationale

We want to have clear, self-evident error reporting in our layers related to synchronization. We have devised a system
to identify 'who' (system), 'where' (phase), and 'what' (category) in order to report problems to the end user, and
ideally a KB article for the user to solve them on their own ('how').

### Goals

- Help end users understand where the problem is and how to fix it. 
- Help Bentley support do an initial triage.

### Schema

See fatal-errors-schema.json

### Transmission format

Since errors contain several pieces of information, encoding the information in JSON should make it easy to produce and
consume across many technologies. Connectors will generate a SyncError.json file upon abnormal termination.

```
{
  version: "1.0",
  errors: [
    {
    system: string,
    phase: string,
    category: string,
    descriptionKey: string,
    description: string,
    kbLink?: string,
    canUserFix: boolean
    }
  ]
}
```

We only expect a single error today, but `errors` is an array for future-proofing.
