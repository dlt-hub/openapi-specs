# Petstore API

>[!NOTE]
>One important thing to note about petstore is that it shows the full list of practical use cases like
>1. Validation,
>2. Type usage,
>3. Using response/request examples,
>4. Standard serial entity IDs,
>5. Security schemes,
>6. JSON, XML and FormData response schemas,
>7. Properly formed additional responses,
>8. Authorization rules

## Security scheme

Auth scheme uses oauth2 which is supported by our rest api client implementation

```yaml
securitySchemes:
    petstore_auth:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: 'https://petstore.swagger.io/oauth/authorize'
          scopes:
            'write:pets': modify pets in your account
            'read:pets': read your pets
    api_key:
      type: apiKey
      name: api_key
      in: header
```

## Handling only JSON type

For example it defines `xml` request/response helpers as below so we need to skip them

```yaml
Customer:
    properties:
    id:
        type: integer
        format: int64
        example: 100000
    username:
        type: string
        example: fehguy
    address:
        type: array
        items:
            $ref: '#/components/schemas/Address'
        xml:
            wrapped: true
            name: addresses
```

## Primary keys

>[!NOTE]
> Some responses schemas like addresses don't have ID fields

Type for primary key is `Int64` and in the response we can simply extract it by `id` field

```yaml
Category:
    x-swagger-router-model: io.swagger.petstore.model.Category
    properties:
        id:
            type: integer
            format: int64
            example: 1
        name:
            type: string
            example: Dogs
        xml:
            name: category
            type: object
```

## Pagination

If the endpoint returns a pagination object it means the endpoint supports pagination - currently it's only possible to change pages with `?page={page_number}` but custom page sizes are not possible.
