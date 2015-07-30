# Behavioral Data

To improve your autocomplete suggestions, you can send three types of behavioral data to Constructor.io: search, click_through, and conversion.

## Track a search

```shell
curl -X POST -H "Content-Type: application/json" -d '{"term":"xyz","num_results":302}' \
  -u "[your token]:" "https://ac.constructor.io/v1/search?autocomplete_key=[your_autocomplete_key]"
```

```javascript
constructorio.track_search({
  term: "xyz",
  num_results: "302"
});
```

The `search` resource should be called whenever a search is performed on your site, together with the search `term` and number of results (`num_results`).

### HTTP Request

`POST https://ac.constructor.io/v1/search?autocomplete_key=[your_autocomplete_key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
term | Yes | The search term the user entered in the search box
num_results | No | The number of total results returned in the search

## Track a click-through

```shell
curl -X POST -H "Content-Type: application/json" -d '{"term":"xyz","item":"Alphabet soup","autocomplete_section":"products_autocomplete"}' \
  -u "[your token]:" "https://ac.constructor.io/v1/click_through?autocomplete_key=[your_autocomplete_key]"
```

```javascript
constructorio.track_click_through({
  term: "xyz",
  item: "Alphabet soup",
  autocomplete_section: "Products"
});
```

The `click_through` resource should be called when a user clicks on a search result (this can often be done from the product detail page). Pass in the search `term` and, optionally, the `item` clicked on so we can learn which items are receiving clicks from which terms and increase their ranking in the autocomplete index. If your autocomplete has multiple sections, also pass in the `autocomplete_section` parameter with the appropriate section name.

### HTTP Request

`POST https://ac.constructor.io/v1/click_through?autocomplete_key=[your_autocomplete_key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
term | Yes | The search term the user entered in the search box
item | No | The autocomplete item that the user clicked on
autocomplete_section | No | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.

## Track a conversion

```shell
curl -X POST -H "Content-Type: application/json" -d '{"term":"xyz","item":"Alphabet soup","autocomplete_section":"products_autocomplete"}' \
  -u "[your token]:" "https://ac.constructor.io/v1/conversion?autocomplete_key=[your_autocomplete_key]"
```

```javascript
constructorio.track_conversion({
  term: "xyz",
  item: " Alphabet soup",
  autocomplete_section: "Products"
});
```

The `conversion` resource should be called when a user purchases a product (or successfully performs another action important to your site). Pass in the search `term` so we can learn which items are receiving conversions and increase their ranking in the autocomplete index. You can also pass in an optional `item` parameter to indicate which item the customer purchased. If your autocomplete has multiple sections, also pass in the `autocomplete_section` parameter with the appropriate section name.

### HTTP Request

`POST https://ac.constructor.io/v1/conversion?autocomplete_key=[your_autocomplete_key]`

### JSON Parameters

Parameter | Required? | Description
--------- | ----------- | ----------
term | Yes | The search term the user entered in the search box
item | No | The autocomplete item that the user clicked on
autocomplete_section | No | Your autocomplete suggestions can have multiple sections like "Products" and "Search Suggestions".  This indicates which section this item is for.
