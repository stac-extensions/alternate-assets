# Alternate Assets Extension Specification

- **Title:** Alternate Assets
- **Identifier:** <https://stac-extensions.github.io/alternate-assets/v1.1.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @matthewhanson

The Alternate Assets extension to STAC provides a way to specify alternate locations (e.g., URLs) for assets.
Sometimes, assets can be retrieved via multiple methods.
For example an asset on AWS may have a public facing http URL but also a direct access s3 URL.
Or an asset is mirrored on multiple servers that have different URLs.
In this case the asset is exactly the same, but different protocols or cloud services may be used to access it.
The content of the asset should be the same, i.e., the checksum of the data should be the same as well as e.g. the media type or the file size.

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](examples/collection.json): Shows usage in Collection assets and [item assets](https://github.com/stac-extensions/item-assets)
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [ ] Collections
- [ ] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name | Type                                                           | Description |
| ---------- | -------------------------------------------------------------- | ----------- |
| alternate  | Map<string, [Alternate Asset Object](#alternate-asset-object)> | An array of alternate location information for an asset |
| name       | string                                                         | A short name to distinguish the asset from the alternate assets. |

Each alternate asset consists of a key and an Alternate Asset Object.

Example:
```json
"alternate": {
  "s3": {
    "href": "s3://bucket/key"
  }
}
```

The Alternate Asset Objects are similar to the
[Asset Object](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md#asset-object)
as defined in the STAC Item Specification.

The key should be used consistently across all assets (and items) if from the same source.
In other words, if all the assets in an Item are all available via s3 direct access, the key for all of them should be the same.

### Alternate Asset Object

The Alternate Asset Object are similar to the core Asset object, except only contain fields relevant to the location and access of the asset. 

| Field Name  | Type   | Description |
| ----------- | ------ | ----------- |
| href        | string | **REQUIRED.** URI to the asset object. Relative and absolute URI are both allowed. |
| name        | string | A short name to distinguish the alternate assets. |

In the simplest case, the object consists of a single `href` field, but could include additional details regarding the alternate location or URL. 

Some fields that are commonly provided:

- `title` and `description` as specified in [STAC's Common Metadata](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#basics).
- The [Storage Extension](https://github.com/stac-extensions/storage) could be used to provide additional details on its host or location.
- The [Authentication Extension](https://github.com/stac-extensions/authentication) could provide details about specific authentication requirements.

It is also recommended that the [Item Assets Definition](https://github.com/stac-extensions/item-assets)
Extension is provided in Collections to convey to users what the options are for alternate access.

The `name` field could potentially also be provided in the core Asset Object as a short name to distinguish them from the alternate assets.

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
