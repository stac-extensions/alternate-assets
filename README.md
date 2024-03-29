# Alternate Assets Extension Specification

- **Title:** Alternate Assets
- **Identifier:** <https://stac-extensions.github.io/alternate-assets/v1.1.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Asset
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Pilot
- **Owner**: @matthewhanson

The Alternate Assets extension to STAC provides a way to specify alternate locations (e.g., URLs) for assets. Sometimes, assets can be retrieved
via multiple methods. For example an asset on AWS may have a public facing http URL but also a direct access s3 URL. Or an asset is mirrored
on multiple servers that have different URLs. In this case the asset is exactly the same, but different protocols or cloud services may be used
to access it.

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](examples/collection.json): Shows usage in Collection assets and [item assets](https://github.com/stac-extensions/item-assets)
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Asset Properties

| Field Name           | Type                      | Description |
| -------------------- | ------------------------- | ----------- |
| alternate         | Map<string, [AlternateAsset Object](#alternate-asset-object)> | An array of alternate location information for an asset |

The Alternate Assets are similar to the core Asset object, except only contain fields relevant to the location and access of the asset. 
In the simplest case, the object consists of a single field, `href`, but could include a title or description to provide additional info
regarding the alternate location or URL. 
The fields from the [Storage Extension](https://github.com/stac-extensions/storage) could be used in an AlternateAsset to 
provide additional details on it's location.

The key to each alternate asset, e.g.,

```json
"alternate": {
  "s3": {
    "href": "s3://bucket/key"
  }
}
```

should be used across all assets if from the same source. In other words, if all the assets
in an Item are all available via s3 direct access, the key for all of them should be the same.

It is also recommended that the [item assets](https://github.com/stac-extensions/item-assets)
extension be used in Collections to convey to users what the options are for alternate access.

### Alternate Asset Object

| Field Name  | Type      | Description |
| ----------- | --------- | ----------- |
| href        | string    | **REQUIRED.** URI to the asset object. Relative and absolute URI are both allowed. |
| title       | string    | The displayed title for clients and users. |
| description | string    | A description of the Asset providing additional details, such as how it was processed or created. [CommonMark 0.29](http://commonmark.org/) syntax MAY be used for rich text representation. |

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
