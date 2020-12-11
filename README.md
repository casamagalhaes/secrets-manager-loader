# Secrets Manager Loader

Retrieves, parses and loads secrets from AWS Secrets Manager directly to process.env

## Example

If your secret prod/myawesomesecret/module value is

```json
{
  "USERNAME": "johndoe",
  "PASSWORD": "hunter2"
}
```

Then this code

```javascript
(async () => {
    await require('secret-manager-loader').load({
        secretId: 'prod/myawesomesecret/module'
    });
    console.log(process.env);
})();
```

Would generate this output
```javascript
{
  //... whatever is in your environment
  USERNAME: 'johndoe',
  PASSWORD: 'hunter2'
}
```

## Requirements

The role or user running the `load` function must have a policy allowing `secretsmanager:GetSecretValue` to the specified secret in `secretId`

## Warning

AWS Secrets Manager is not free (https://aws.amazon.com/secrets-manager/pricing/), each call to `load` means an API call, so don't overdo it. You should think of a caching strategy to avoid any problems on frequent workloads.
