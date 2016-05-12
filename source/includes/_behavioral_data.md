# Behavioral Data

To improve your autocomplete suggestions, you can send three types of behavioral data to Constructor.io: search, click_through, and conversion.

## Track a search

```shell
curl -X POST -H "Content-Type: application/json" -d '{"term":"xyz","num_results":302}' \
  -u "[your token]:" "https://ac.cnstrc.com/v1/search?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.track_search({
  term: "xyz",
  num_results: "302"
});
```

```ruby
response = constructorio.track_search({
  term: "xyz",
  num_results: "302"
});
```

```python
response = constructor_instance.track_search(
    term="xyz",
    num_results=302)
```

```php
<?php
$response = $constructor->trackSearch(
  "xyz", // term name
  array("num_results" => 302) // array of properties of the search
);
```

```perl
my $response = $constructorio->track_search(
  term => "xyz",
  num_results => 302
);
```

```java
boolean success = constructorio.trackSearch("xyz", 302);
// "xyz" is the term that was searched
// 302 is the number of results
```

```csharp
bool success = constructorio.TrackSearch("xyz", 302);
// "xyz" is the term that was searched
// 302 is the number of results
```

The `search` resource should be called whenever a search is performed on your site, together with the search `term` and number of results (`num_results`).

### HTTP Request

`POST https://ac.cnstrc.com/v1/search?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
term | Yes | The search term the user entered in the search box
num_results | No | The number of total results returned in the search

## Track a click-through

```shell
curl -X POST -H "Content-Type: application/json" -d '{"term":"xyz","item":"Alphabet soup","autocomplete_section":"Search Suggestions"}' \
  -u "[your token]:" "https://ac.cnstrc.com/v1/click_through?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.track_click_through({
  term: "xyz",
  item: "Alphabet soup",
  autocomplete_section: "Search Suggestions"
});
```

```ruby
response = constructorio.track_click_through({
  term: "xyz",
  item: "Alphabet soup",
  autocomplete_section: "Search Suggestions"
});
```

```python
response = constructor_instance.track_click_through(
    term="xyz",
    autocomplete_section="Search Suggestions")
```

```php
<?php
$response = $constructor.trackClickThrough(
  "xyz", // term name
  "Search Suggestions", // autocomplete section name
  array("item" => "power drill") // array of properties of the click through
);
```

```perl
my $response = $constructorio->track_click_through(
  term => "xyz",
  item => "Alphabet soup",
  autocomplete_section => "Search Suggestions"
);
```

```java
boolean success = constructorio.trackClickThrough("xyz", "alphabet soup", "Search Suggestions");
// xyz is the term
// alphabet soup is the item
// Search Suggestions is the autocomplete section
```

```csharp
bool success = constructorio.TrackClickThrough("xyz", "alphabet soup", "Search Suggestions");
// xyz is the term
// alphabet soup is the item
// Search Suggestions is the autocomplete section
```

The `click_through` resource should be called when a user clicks on a search result (this can often be done from the product detail page). Pass in the search `term` and, optionally, the `item` clicked on so we can learn which items are receiving clicks from which terms and increase their ranking in the autocomplete index. Beacuse your autocomplete can have multiple sections, you must also pass in the `autocomplete_section` parameter with the appropriate section name.

### HTTP Request

`POST https://ac.cnstrc.com/v1/click_through?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
term | Yes | The search term the user entered in the search box
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.
item | No | The autocomplete item that the user clicked on

## Track a conversion

```shell
curl -X POST -H "Content-Type: application/json" -d '{"term":"xyz","autocomplete_section":"Search Suggestions","item":"Alphabet soup"}' \
  -u "[your token]:" "https://ac.cnstrc.com/v1/conversion?autocomplete_key=[your autocomplete key]"
```

```javascript
constructorio.track_conversion({
  term: "xyz",
  autocomplete_section: "Search Suggestions",
  item: "Alphabet soup"
});
```

```ruby
response = constructorio.track_conversion({
  term: "xyz",
  autocomplete_section: "Search Suggestions",
  item: "Alphabet soup"
});
```

```python
response = constructor_instance.track_conversion(
    term="xyz",
    autocomplete_section="Search Suggestions",
    item="Alphabet Soup")
```

```php
<?php
$response = $constructor.trackConversion(
  "xyz", // term name
  "Search Suggestions", // autocomplete section name
  array("item" => "power drill") // array of properties of the conversion
);
```

```perl
my $response = $constructorio->track_conversion(
  term => "xyz",
  autocomplete_section => "Search Suggestions",
  item => "Alhabet Soup"
);
```

```java
boolean success = constructorio.trackConversion("xyz", "Search Suggestions");
// xyz is the term
// Search Suggestions is the autocomplete section
```

```csharp
bool success = constructorio.TrackConversion("xyz", "Search Suggestions");
// xyz is the term
// Search Suggestions is the autocomplete section
```

The `conversion` resource should be called when a user purchases a product (or successfully performs another action important to your site). Pass in the search `term` so we can learn which items are receiving conversions and increase their ranking in the autocomplete index. You can also pass in an optional `item` parameter to indicate which item the customer purchased. Because your autocomplete can have multiple sections, you must also pass in the `autocomplete_section` parameter with the appropriate section name.

### HTTP Request

`POST https://ac.cnstrc.com/v1/conversion?autocomplete_key=[your autocomplete key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
term | Yes | The search term the user entered in the search box
autocomplete_section | Yes | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.  See [your dashboard](/dashboard) for the section names to use.
item | No | The item that the user purchased
revenue | No | The purchase amount in cents (that is, the dollar amount * 100)

### Via Javascript

Conversions can also be tracked via Javascript, like so:

<code>
&lt;script type="text/javascript" src="//cnstrc.com/js/ac.js">&lt;/script>
&lt;script&gt;<br/>
window['constructorio'] = window['constructorio'] || [];<br/>
window['constructorio'].push(["trackEvent", "purchase", {<br/>
&nbsp;&nbsp;"autocomplete_key": "[your autocomplete key]",<br/>
&nbsp;&nbsp;"revenue": [the purchase amount in cents],<br/>
&nbsp;&nbsp;"term": "[the search term the user entered in the search box]",<br/>
&nbsp;&nbsp;"item": "[the item that the user purchased]",<br/>
&nbsp;&nbsp;"autocomplete_section": "[the autocomplete section]"<br/>
}]);<br/>
&lt;/script>
</code>

Note that if `term`, `item`, and `autocomplete_section` are ommitted, the Javascript client will populate them with its own tracking information.
