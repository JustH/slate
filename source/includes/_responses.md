# Responses


```shell
# shell responses will return raw JSON
```

```javascript
// responses and errors that return data are JSON structures
console.log(response.message);
console.log(error.message);
```

```ruby
# responses are Faraday objects with JSON bodies
puts response.status # print the status code
puts JSON(response.body)["message"]
```

```python
# responses are converted to dictionaries for your convenience
response = constructor_instance.verify()
print response
# {u'message': u'successful authentication'}
```

```php
<?php
// responses are converted to arrays for your convenience
$response = $constructor->verify();
print_r($response);
// {
//   "message": "successful authentication"
// }
```

```perl
# responses are HTTP::Response objects
my $response = $constructorio->verify();
```

Most successful responses return 204 No Data codes without any further information.

Responses and errors that return data are JSON structures that will contain a "message" parameter with more information.
