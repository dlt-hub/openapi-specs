# Quotes API

## Primary keys

>[!NOTE]
> Some responses schemas like categories don't have ID fields

Type for primary key is `Int64` and in the response we can simply extract it by `id` field

## Security

Bearer token auth is used to authentication requests

## Pagination

Used pagination is of offset limit type with the following parameters

1. `limit` - how many records to show,
2. `start` - offset value.
