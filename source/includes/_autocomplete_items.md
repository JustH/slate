# Autocomplete Items

Suggestions that are shown in the autocomplete results are called `items`.  `items` can be full product names (with metadata including images and descriptions) or simple search terms.

## Add an Item

```shell
curl -X POST -H "Content-Type: application/json" \
  -d '{"item_name":"power drill","keywords":["battery-powered","drills","drywall"],
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
<?php
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
ListItem item = new ListItem(
  Name: "Power drill",
  Description: "Like a drill, with power.",
  URL: "http://constructor.io/power-drill",
  ImageURL: "http://constructor.io/power-drill.jpg",
  AutocompleteSection: "Products"
);

bool success = ConstructorIOAPI.Add(item);

// "item" is a ListItem containing key / value pairs as specified
// in parameters below.
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

## Add or Update an Item

```shell
curl -X PUT -H "Content-Type: application/json" \
  -d '{"item_name":"power drill","keywords":["battery-powered","drills","drywall"],
  "suggested_score":36,"url":"http://www.mysite.com/power_drill","autocomplete_section":"Search Suggestions"}' \
  -u"[your token]:" "https://ac.cnstrc.com/v1/item?force=1&autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.add_or_update(
  { item_name: "power drill", autocomplete_section: "Search Suggestions" },
  function(error, response) {
    if (error) {
      console.log(error);
    }
  }
);
```

```ruby
response = constructorio.add_or_update(
  { item_name: "power drill", autocomplete_section: "Search Suggestions" }
);
```

```python
response = constructor_instance.add_or_update(
    item_name="power drill",
    autocomplete_section="Search Suggestions")
```

```php
<?php
$response = $constructor->addOrUpdate(
  "power drill", // item name
  "Search Suggestions" // autocomplete section name
);
```

```perl
my $response = $constructorio->add_or_update(
  item_name => "power drill",
  autocomplete_section => "Search Suggestions"
);
```

```java
boolean success = constructorio.addOrUpdate("power drill", "Search Suggestions");
// power drill is an item name
// Search Suggestions is an autocomplete section name
```

```csharp
ListItem item = new ListItem(
  Name: "Power drill",
  Description: "Like a drill, with power.",
  URL: "http://constructor.io/power-drill",
  ImageURL: "http://constructor.io/power-drill.jpg",
  AutocompleteSection: "Products"
);

bool success = ConstructorIOAPI.AddOrUpdate(item);

// "item" is a ListItem containing key / value pairs as specified
//   in parameters below. If an item with the name "Power drill"
//   already exists, its Description, Url and ImageUrl will be
//   updated as indicated. Otherwise a new item will be created
//   with these values.
```


 > The above commands return a 204 Success response on success.

An add or update operation (also known as an `UPSERT`) updates an item in your autocomplete index if it already exists, or adds the item to your index if it does not yet exist. 

To add or update an item in your autocomplete index, use the `POST /item` call, with `?force=1`. Options are the same as for the standard `Add an Item` call: `item_name` and `autocomplete_section` are required and all other parameters are optional.

We determine whether an item already exists based on the optional `id` set for the item, or if not present, the `item_name` and `autocomplete_section`.

### HTTP Request

`PUT https://ac.cnstrc.com/v1/item?force=1&autocomplete_key=[your autocomplete key]`

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
  -d '{"items": [ {"item_name": "power drill"}, {"item_name": "hammer"} ],
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

```python
# This method is not currently supported in our python client.
```

```php
<?php
$response = $constructor->addBatch(
  array("power drill", "hammer"),
  "Search Suggestions"
);

$toolBox = array(
   array("item_name" => "power drill", "url" => "/products/power-drill", "image_url" => "/images/power-drill.jpg"),
   array("item_name" => "hammer", "url" => "/products/hammer", "image_url" => "/images/hammer.jpg")
);
$response = $constructor->addBatch($toolBox, "Products");
```

```perl
my $response = $constructorio->add_batch(
  items => [ { item_name => "power drill" }, { item_name => "hammer" } ],
  autocomplete_section => "Search Suggestions"
);
```

```java
boolean success = constructorio.addBatch("Search Suggestions", "power drill", "hammer");
// "Search Suggestions" is an autocomplete section name
// power drill is an item name
// hammer is an item name
```

```csharp
List<ListItem> itemList = new List<ListItem>();

itemList.Add(new ListItem(
  Name: "Power drill",
  Description: "Like a drill, with power.",
  URL: "http://constructor.io/power-drill",
  ImageURL: "http://constructor.io/power-drill.jpg"
));

itemList.Add(new ListItem(
  Name: "Hammer",
  Description: "When everything looks like a nail.",
  URL: "http://constructor.io/hammer"
));

bool success = ConstructorIOAPI.AddBatch(itemList, "Products");

// itemList is a List<ListItem> composed of key / value pairs as
//   specified in parameters below.
// "Products" is the  autocomplete section to which you'd like to
//   add the items contained in itemList
```

> The above command(s) return a 204 Success response on success.

To add multiple items to your autocomplete index as a batch, use the `POST /batch_items` call. The `items` parameter is required and is a list of items with the same attributes as defined in the [Add an Item](#add-an-item) resource.  Because your autocomplete can have multiple sections, like categories, search suggestions, and direct links to products, you must specify which section you are adding an item to. You can do this with the `autocomplete_section` parameter.

### HTTP Request

`POST https://ac.cnstrc.com/v1/batch_items?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ------- | -----------
items | Yes | A list of items with the same attributes as defined in the [Add an Item](#add-an-item) resource
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.

## Batch Add or Update Items

```shell
curl -X PUT -H "Content-Type: application/json" \
  -d '{"items": [ {"item_name": "power drill"}, {"item_name": "hammer"} ],
    "autocomplete_section":"Search Suggestions"}' \
  -u"[your token]:" "https://ac.cnstrc.com/v1/batch_items?force=1&autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.add_or_update_batch(
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
response = constructorio.add_or_update_batch(
  {
    items: [
      { item_name: "power drill" },
      { item_name: "hammer" }
    ],
    autocomplete_section: "Search Suggestions"
  }
);
```

```php
<?php
$response = $constructor->addOrUpdateBatch(
  array("power drill", "hammer"),
  "Search Suggestions"
);

$toolBox = array(
   array("item_name" => "power drill", "url" => "/products/power-drill", "image_url" => "/images/power-drill.jpg"),
   array("item_name" => "hammer", "url" => "/products/hammer", "image_url" => "/images/hammer.jpg")
);
$response = $constructor->addOrUpdateBatch($toolBox, "Products");
```

```perl
my $response = $constructorio->add_or_update_batch(
  items => [ { item_name => "power drill" }, { item_name => "hammer" } ],
  autocomplete_section => "Search Suggestions"
);
```

```java
boolean success = constructorio.addOrUpdateBatch("Search Suggestions", "power drill", "hammer");
// power drill is an item name
// hammer is an item name
// Search Suggestions is an autocomplete section name
```

```csharp
List<ListItem> itemList = new List<ListItem>();

itemList.Add(new ListItem(
  Name: "Power drill",
  Description: "Like a drill, with power.",
  URL: "http://constructor.io/power-drill",
  ImageURL: "http://constructor.io/power-drill.jpg"
));

itemList.Add(new ListItem(
  Name: "Hammer",
  Description: "When everything looks like a nail.",
  URL: "http://constructor.io/hammer"
));

bool success = ConstructorIOAPI.AddOrUpdateBatch(itemList, "Products");

// itemList is a List<ListItem> composed of key / value pairs as
//   specified in parameters below. If "Power drill" or "Hammer"
//   already exist, their metadata will be updated as above.
//   Otherwise new items will be created with these values.
// "Products" is the  autocomplete section to which you'd like to
//   add the items contained in itemList
```

> The above command(s) return a 204 Success response on success.

A batch add or update allows you to add a group of items to your autocomplete without first checking to make sure no item in the batch already exists.

Any items that don't already exist are created, and any items that already exist are updated. This is also known as an `UPSERT` operation.

To add or update a batch of items to your autocomplete index, use the `PUT /batch_items` call, with `?force=1`. Options are the same as for the standard `Batch Add Items` call: `item_name` and `autocomplete_section` are required and all other parameters are optional.

We determine whether items already exist based on the `item_name` and `autocomplete_section` set for each item. However, if the optional `id` parameter is set for the items, we determine whether items already exist using this parameter.

### HTTP Request

`PUT https://ac.cnstrc.com/v1/batch_items?force=1&autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ------- | -----------
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.
items | Yes | A list of items with the same attributes as defined in the [Add an Item](#add-an-item) resource

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
<?php
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
ListItem item = new ListItem(
  Name: "Power drill",
  AutocompleteSection: "Products"
);

bool success = ConstructorIOAPI.Remove(item);

// "item" is a ListItem with the Name or ID for the item you'd
//   like to remove
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

## Batch Remove Items

```shell
curl -X DELETE -H "Content-Type: application/json" -d {"items": [ {"item_name": "power drill"}, {"item_name": "hammer"} ],
    "autocomplete_section":"Search Suggestions"}' \
  -u "[your token]:" "https://ac.cnstrc.com/v1/batch_items?autocomplete_key=[your autocomplete key]"
```

```javascript
// This method is not currently supported in our javascript client.
```

```ruby
# This method is not currently supported in our ruby client.
```

```python
# This method is not currently supported in our python client.
```

```php
<?php
// This method is not currently supported in our php client.
```

```perl
# This method is not currently supported in our perl client.
```

```java
// This method is not currently supported in our java client.
```

```csharp
List<ListItem> itemList = new List<ListItem>();

itemList.Add(new ListItem(Name: "Power drill"));
itemList.Add(new ListItem(ID: "245"));

bool success = ConstructorIOAPI.RemoveBatch(itemList, "Products");

// itemList is a List<ListItem> with the IDs and/or Names of
//   the items you'd like to remove.
// "Products" is an autocomplete section name.
```
> The above command returns a 204 Success response on success.

To remove multiple items from your autocomplete index as a batch, use the `DELETE /batch_items` call. Note: this will remove all meta-information such as keywords we currently store on the items.

The `items` parameter is required and is a list of items with the same attributes as defined in the [Remove an Item](#remove-an-item) resource. If your autocomplete has multiple sections (i.e. products, categories, and search suggestions), you must specify the name of the autocomplete section from which you're removing the items.

### HTTP Request

`DELETE https://ac.cnstrc.com/v1/batch_items?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
items | Yes | A list of items with the same attributes as defined in the [Remove an Item](#remove-an-item) resource.
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.

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
<?php
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
ListItem item = new ListItem(
  Name: "Drill",
  URL: "http://constructor.io/drill",
  AutocompleteSection: "Products"
);

item.Name = "Power drill";
item.Description = "Like a drill, with power."

bool success = ConstructorIOAPI.Modify(item);
// "Drill" is the original item name as you previously saved it
//   in our system
// "Power drill" is the new item name
// "Description" is a new description to add for the item
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
