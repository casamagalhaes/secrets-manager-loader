# Secret Manager Loader

Parses and loads secrets from AWS Secret Manager directly to process.env

## Example

```javascript
(async () => {
    await require('secret-manager-loader').load({
        secretId: 'prod/myawesomesecret/module'
    });
    // Make the magic happen
})();
```

## Requirements

The role or user running the `load` function must have a policy allowing `secretsmanager:GetSecretValue` to the specified secret in `secretId`
