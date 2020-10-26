# Errors

The OpenTitles API uses the following error codes:

Error Code | Meaning
---------- | -------
404 | Not Found -- The specified resource could not be found. Formatted as JSON with an error property describing the error and a lookat property with the path to a list of this resource.
500 | Internal Error -- An error occured on the server side that could not be recovered from.

```json
{
  'error': 'No such country',
  'lookat': '/v2/country'
}
```