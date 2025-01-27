# View Promotion

Fire whenever a user sees a promotion link.

Promotions do not have a solid definition at the moment and are likely to be defined by the site owners. Additionally, the method in which Google's default reports will display them is still vague. As such, setting this is very contextual. For the moment, don't implement this event. We will let you know when it's more clear.

## HTML Data Attributes

```html
<a href="<link_url>"
  data-layer-event="view_promotion"
  data-layer-facets="<facets>"
  data-layer-list_type="<list_type>"
  data-layer-search_term="<search_term>"
  data-layer-search_term="<search_type>"
  data-layer-index="<index>"
>
```

## Javascript Code

```js
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_promotion",
  ecommerce: {
    facets: "<facets>",
    item_id: "<item_id>",
    list_type: "<list_type>",
    search_term: "<search_term>",
    search_type: "<search_type>",
    index: "<index>",
    items: "<items>"
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Pattern|Min Length|Max Length|Minimum|Maximum|Multiple Of|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|facets|delimited string|contextual|A double-delimited string of key/value pairs representing the refinements that were applied to this search. Only set if the list type is a search result or filter_by_group.|category:skin_health~skin_concern:acne~featured_as:best_seller|
|item_id|string|recommended|
|list_type|string|contextual|The type of list the item was found in.|cards, carousel, popular_products, search_results|
|search_term|string|contextual|The final search term submitted after any correction has been performed. Only set if the `list_type` is `search_results`.|sunscreen|
|search_type|string|contextual|The type of search performed. Only set if the `list_type` is `search_results`.|site, filter_by_group|
|index|integer|required|The numerical index of the item position (1-indexed). For instance, if this is the 5th search result, you would send 5 here. If this is the 3rd card in a single row, send 3. If this is the 2nd item in the 3rd row of a 3-up card layout, send 8 (3 + 3 + 2).|5|
|items|array of [items](/schemas/item.md)|required|Populate with item objects that represent the product viewed.|[{item_id: "test"}]
