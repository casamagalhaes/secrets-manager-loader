# Secret Manager Loader

Parses and loads secrets from AWS Secret Manager directly to process.env

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
