# Autocomplete Items

Suggestions that are shown in the autocomplete results are called `items`.  `items` can be full product names (with metadata including images and descriptions) or simple search terms.

## Add an Item

```shell
curl -X POST -H "Content-Type: application/json" \
  -d '{"item_name":"power drill","keywords":["battery-powered","drills","drywall"], \
  "suggested_score":36,"url":"http://www.mysite.com/power_drill","autocomplete_section":"Search Suggestions"}' \
  -u"[your token]:" "https://ac.cnstrc.com/v1/item?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.add(
  { item_name: "power drill", autocomplete_section: "Search Suggestions" },
  function(error, response) {
    if (error) {
      console.log(error);
    }
  }
);
```

```ruby
response = constructorio.add(
  { item_name: "power drill", autocomplete_section: "Search Suggestions" }
);
```

```python
response = constructor_instance.add(
    item_name="power drill",
    autocomplete_section="Search Suggestions")
```

```php
$response = $constructor->add(
  "power drill", // item name
  "Search Suggestions" // autocomplete section name
);
```

```perl
my $response = $constructorio->add(
  item_name => "power drill",
  autocomplete_section => "Search Suggestions"
);
```

```java
boolean success = constructorio.add("power drill", "Search Suggestions");
// power drill is an item name
// Search Suggestions is an autocomplete section name
```

```csharp
bool success = constructorio.Add("power drill", "Search Suggestions");
// power drill is an item name
// Search Suggestions is an autocomplete section name
```

> The above command returns a 204 Success response on success.

To add an item to your autocomplete index, use the `POST /item` call. The `item_name` is required. You can also pass in an optional `suggested_score` between 1-100, which will influence the item's initial ranking relative to other item scores (the higher the score, the higher in the list of suggestions the item will appear). You can also optionally pass in the item's `keywords` to give us more meta information and help us better determine how and where to display the item when autocompleting. If you would like to add an item that points to a direct link, just pass in that link as a `url`. Finally, because your autocomplete can have multiple sections, like categories, search suggestions, and direct links to products, you must specify which section you are adding an item to. You can do this with the `autocomplete_section` parameter.

### HTTP Request

`POST https://ac.cnstrc.com/v1/item?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ------- | -----------
item_name | Yes | The name of the item, as it will appear in the autocomplete suggestions
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.
suggested_score | No | A number between 1-100 that will influence the item's initial ranking relative to other item scores (the higher the score, the higher in the list of suggestions the item will appear)
keywords | No | An array of keywords for this item.  Keywords are useful if you want a product name to appear when a user enters a searchterm that isn't in the product name iteslf.
url | No | A URL to directly send the user after selecting the item
image_url | No | A URL that points to an image you'd like displayed next to some item (only applicable when url is supplied)
description | No | A description for some item (only applicable when url is supplied)
id | No | An arbitrary ID you would like associated with this item.  You can use this field to store your own IDs of the items to more easily access them in other API calls.

## Batch Add Items

```shell
curl -X POST -H "Content-Type: application/json" \
  -d '{"items": [ {"item_name": "power drill"}, {"item_name": "hammer"} ],\
    "autocomplete_section":"Search Suggestions"}' \
  -u"[your token]:" "https://ac.cnstrc.com/v1/batch_items?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.add_batch(
  {
    items: [
      { item_name: "power drill" },
      { item_name: "hammer" }
    ],
    autocomplete_section: "Search Suggestions"
  },
  function(error, response) {
    if (error) {
      console.log(error);
    }
  }
);
```

```ruby
response = constructorio.add_batch(
  {
    items: [
      { item_name: "power drill" },
      { item_name: "hammer" }
    ],
    autocomplete_section: "Search Suggestions"
  }
);
```

```perl
my $response = $constructorio->add_batch(
  items => [ { item_name => "power drill" }, { item_name => "hammer" } ],
  autocomplete_section => "Search Suggestions"
);
```

> The above command returns a 204 Success response on success.

To add multiple items to your autocomplete index as a batch, use the `POST /batch_items` call. The `items` parameter is required and is an array of item hashes with the same attributes as defined in the `Add an Item` resource.  Because your autocomplete can have multiple sections, like categories, search suggestions, and direct links to products, you must specify which section you are adding an item to. You can do this with the `autocomplete_section` parameter.

### HTTP Request

`POST https://ac.cnstrc.com/v1/batch_items?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ------- | -----------
items | Yes | An array of item hashes with the same attributes as defined in the `Add an Item` resource
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.

## Remove an Item

```shell
curl -X DELETE -H "Content-Type: application/json" -d '{"item_name":"power drill","autocomplete_section":"products_autocomplete"}' \
  -u "[your token]:" "https://ac.cnstrc.com/v1/item?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.remove(
  { item_name: "power drill", autocomplete_section: "Search Suggestions" },
  function(error, response) {
    if (error) {
      console.log(error);
    }
  }
);
```

```ruby
response = constructorio.remove(
  { item_name: "power drill", autocomplete_section: "Search Suggestions" }
);
```

```python
response = constructor_instance.remove(item_name="power drill", autocomplete_section="Search Suggestions")
```

```php
$response = $constructor->remove(
  "power drill", // item name
  "Search Suggestions" // autocomplete section name
);
```

```perl
my $response = $constructorio->remove(
  item_name => "power drill",
  autocomplete_section => "Search Suggestions"
);
```

```java
boolean success = constructorio.remove("power drill", "Search Suggestions");
// power drill is an item name
// Search Suggestions is an autocomplete section name
```

```csharp
bool success = constructorio.Remove("power drill", "Search Suggestions");
// power drill is an item name
// Search Suggestions is an autocomplete section name
```

> The above command returns a 204 Success response on success.

To remove an item from your autocomplete index (if, for instance, a product has been discontinued), issue a `DELETE /item` call. Note: this will remove all meta-information such as keywords we currently have on the item. If your autocomplete has multiple sections (i.e. products, categories, and search suggestions), you must specify the name of the autocomplete section from which you're removing an item.

### HTTP Request

`DELETE https://ac.cnstrc.com/v1/item?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
item_name | Yes | The name of the item, as it will appear in the autocomplete suggestions
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.
id | No | An arbitrary ID you optionally specified when adding the item.  If passed in, you don't need to pass in item_name.

## Modify an Item

```shell
curl -X PUT -H "Content-Type: application/json" -d '{"item_name":"power drill","new_item_name":"super power drill","keywords":["concrete","power tools","drills","drywall"],"suggested_score":20,"url":"http://www.mysite.com/power_drill","autocomplete_section":"products_autocomplete"}' \
  -u "[your token]:" "https://ac.cnstrc.com/v1/item?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.modify(
  {
    item_name: "power drill",
    new_item_name: "super power drill",
    autocomplete_section: "Search Suggestions",
    url: "http://www.mysite.com/power_drill",
  },
  function(error, response) {
    if (error) {
      console.log(error);
    }
  }
);
```

```ruby
response = constructorio.modify(
  {
    item_name: "power drill",
    new_item_name: "super power drill",
    autocomplete_section: "Search Suggestions",
    url: "http://www.mysite.com/power_drill",
  }
);
```

```python
response = constructor_instance.modify(
    item_name="power drill",
    new_item_name="better power drill",
    autocomplete_section="Search Suggestions",
    url="http://www.mysite.com/power_drill")
```

```php
$response = $constructor->modify(
  "power drill", // item name
  "super power drill", // new item name (this is required)
  "Search Suggestions", // autocomplete section name
  array("suggested_score" => 100) // array of item properties to modify
);
```

```perl
my $response = $constructorio->modify(
  item_name => "power drill",
  new_item_name => "super power drill",
  autocomplete_section => "Search Suggestions",
  url => "http://www.mysite.com/power_drill"
);
```

```java
boolean success = constructorio.modify("power drill", "super power drill", "Search Suggestions", paramMap);
// power drill is an item name
// super power drill is an item name
// Search Suggestions is an autocomplete section name
// paramMap is a Map<String, Object> you filled beforehand with the other properties you want to modify. Optional.
```

```csharp
bool success = constructorio.Modify("power drill", "super power drill", "Search Suggestions", paramDict);
// power drill is an item name
// super power drill is the new item name
// Search Suggestions is an autocomplete section name
// paramDict is a Dictionary<string, object> you filled beforehand with the other properties you want to modify, it can be null
```

> The above command returns a 204 Success response on success.

To modify an item already in your autocomplete index, use the `PUT /item` call. The `item_name` is required. You can also pass in an optional `suggested_score` between 1-100, which will influence the item's initial ranking relative to other item scores (the higher the score, the higher in the list of suggestions the item will appear). You can also optionally pass in the item's `keywords` to give us more meta information and help us better determine how and where to display the item when autocompleting. If the item should point to a direct link, just pass in that link as a `url`. Finally, because your autocomplete can have multiple sections, like categories, search suggestions, and direct links to products, you must specify in which section you are modifying an item. You can do this with the `autocomplete_section` parameter.

Note: modifying an item replaces all meta information, such as keywords, we previously had on the item, but does not update the score unless you provide a new suggested_score.

### HTTP Request

`PUT https://ac.cnstrc.com/v1/item?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
item_name | Yes | The name of the item, as it currently appears in the autocomplete suggestions
new_item_name | Yes | The name of the item, as it you'd like it to appear in the autocomplete suggestions
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.
suggested_score | No | A number between 1-100 that will influence the item's initial ranking relative to other item scores (the higher the score, the higher in the list of suggestions the item will appear)
keywords | No | An array of keywords for this item.  Keywords are useful if you want a product name to appear when a user enters a searchterm that isn't in the product name iteslf.
url | No | A URL to directly send the user after selecting the item
image_url | No | A URL that points to an image you'd like displayed next to some item (only applicable when url is supplied)
description | No | A description for some item (only applicable	when url is supplied)
id | No | An arbitrary ID you optionally specified when adding the item.  If passed in, you don't need to pass in item_name.
