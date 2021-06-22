# Alternate Assets Extension Specification

- **Title:** Alternate Assets
- **Identifier:** <https://stac-extensions.github.io/alternate-assets/v1.0.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Asset
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @matthewhanson

The Alternate Assets extension to STAC provides a way to specify alternate locations (e.g., URLs) for assets. Sometimes, assets can be retrieved
via multiple methods. For example an asset on AWS may have a public facing http URL but also a direct access s3 URL. Or an asset is mirrored
on multiple servers that have different URLs. In this case the asset is exactly the same, but different protocols or cloud services may be used
to access it.

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Asset Properties

| Field Name           | Type                      | Description |
| -------------------- | ------------------------- | ----------- |
| alternate         | [[Asset Object](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md#asset-object)] | An array of alternate location information for an asset |

The alternate Assets are like any other Asset object, except should only contain fields relevant to the location and access of the asset. 
In the simplest case, the object consists of a single field, `href`, but could include other fields if they do not specify
attributes in the physical asset. For example, `gsd` represents the resolution of the data asset. Changing that would imply
a different asset. Fields like `title` or `description` can be used to provide info on the alternate asset.
Considering other extensions, the fields from the [Storage Extension](https://github.com/stac-extensions/storage) 
could be used in an alternative asset to provide additional details on it's location.

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
