## Importing Assets
Before you submit this mutation request, you must configure an Asset custom source. For more information and an example workflow, see ![Tanium Asset User Guide: Create an Import API source](https://docs.tanium.com/asset/asset/sources.html#import_api)
> If the request is structurally and syntactically valid, each asset object imports separately. A failed asset import does not prevent other valid asset objects in that request from importing.

The following example Asset custom source, named test-name, defines two field mappings for computer_name and serial_number and defines computer_name as a key field.

```json
{
  "keys": [
    "computer_name"
  ],
  "fieldMaps": [
    {
      "destination": "computer_name",
      "source": "computerName"
    },
    {
      "destination": "serial_number",
      "source": "serialNumber"
    }
  ]
}
```

Create variables to match the custom source you created
```json
{
  "source": "test-name",
  "json": "[{\"computerName\": \"computer123\", \"serialNumber\": \"testSerial123\"}, {\"computerName\": \"computer234\", \"serialNumber\": \"testSerial234\"}]"
}
```

Create a mutation to take your variables and import them into your custom source

```typescript
mutation importAssets($source: String!, $json: String!) {
  assetsImport(input: {sourceName: $source, json: $json}) {
    assets {
      id
      index
      status
    }
  }
}
```
