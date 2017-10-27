# The Manifest System: Next Steps

This document constitutes something like a report on the current state of the Manifest System and where it needs to go.

** Last Update: Oct 27, 2017**

## Road Map

- [ ] Improve the documentation. It's not bad, but it could be better, and changes will have to be made anyway based on recent developments.
- [ ] Re-evaluate the property keywords in the spec to ensure that they are as descriptive and consistent as possible.
- [ ] Develop a full JSON schema description of the spec (this has only been done partially, and it will have to change based on the above).
- [ ] Create a manifest type for "projects" in order to make the manifest system integrate with the Virtual Workspace.
- [ ] Create a formal description of the integration of the WE1S manifest system with the Jupyter Notebooks spec.
- [ ] Consider integrating the WE1S spec with the Frictionless Data container format. This could be as minor as tweaking a few property keywords or mapping keywords for crosswalking or making the WE1S manifest system a formal extension of Frictionless Data.
- [ ] Bring all of the above to a polished enough state that we can formally present it to the advisory board for feedback.

Each of these tasks is discussed in more detail below:

## Documentation

Mostly, the documentation needs to be brought up to date and given more consistent terminology and formatting. It is possible that RFC-style formatting should be used, but, in general, the documentation needs to be made easier to use for humanists. Perhaps a dedicated website using GitHub pages might be employed.

## Manifest Schema Vocabulary

In some cases, keywords were adopted arbitrarily with the understanding that they would be re-evaluated later. Although this may be something of an ongoing process, now is the time to begin. One example (mentioned below) is the use of `Publications` for the root of our published sources. It may be worth considering a more generically applicable term, such as `sources`.

## JSON Schema

At present, we don't have any published formal description, although we will eventually need one to fully implement the Workflow Management System and to validate manifests. The main reason for this is that writing up the schema in JSON Schema format is time consuming. But we should probably start doing it as we begin to revise the specification. Standards like Frictionless Data require a formal specification in JSON Schema format, which makes it additionally valuable for crosswalking purposes. I believe [this](https://github.com/jupyter/nbformat/blob/master/nbformat/v4/nbformat.v4.schema.json) is the latest version for Jupyter Notebooks.

## Project Manifests

In the original manifest schema, it was assumed that every data `collection` would function as a type of project. However, there are good reasons to segregate instances of the data in the WE1S `Corpus` from the `collection`s therein. The main reason is that this is what the Virtual Workspace does; it creates a project folder and clones the `collection` data inside. In order to integrate the manifest system and the Virtual Workspace, a `Project` manifest type should be created so that the Virtual Workspace can generate project data and metadata that are compatible with the manifest specs and that can be easily imported or exported from the WE1S database. A `Project` manifest would serve as the root node for collections, publications, and processes that would then be copied from the overall WE1S superstructure (or from elsewhere if the system is being adapted by others). A draft proposal for Project manifests is available at [https://github.com/whatevery1says/manifest/blob/master/project-manifests-draft.md](https://github.com/whatevery1says/manifest/blob/master/project-manifests-draft.md), although it now needs some updating.

## Integrating the WE1S Manifest System with Jupyter Notebooks

Jeremy and I decided that the two systems would be best integrated if the Jupyter Notebook lived inside a `Project` with its own manifest. The content of the project would be described using manifests, and the Jupyter Notebook would contain the scripts to implement the workflow by reading and writing content from/to manifests (as well as writing other output files). I am not 100% sure how this is handled. Does that make the Jupyter Notebook itself a `Process` in the `Project`? Its function is something akin to a `cwl-runner` in the [Common Workflow Language](http://www.commonwl.org/user_guide/02-1st-example/) (which is a useful point of comparison). It is possible that it should be a property of the `Project` node. But should the Jupyter Notebook itself contain any WE1S metadata properties?

## Integrating the WE1S Manifest System with Frictionless Data

[Frictionless Data](http://frictionlessdata.io/) is a project that is developing a set of tools, standards, and best practices for publishing data. It thus shares a similar motivation (as well as similar technologies) to WE1S's manifest system. Frictionless Data provides a standard for describing data resources, which can be gathered togethe in a container format called a [Data Package](http://frictionlessdata.io/data-packages/). Like WE1S, Frictionless Data makes use of JSON manifests. The central difference is that a manifest _must_ be in JSON format and the Data Package root manifest _must_ be called `datapackage.json`.

Whilst Frictionless Data Data Packages are not concerned with the whole workflow, their format and function is very similar to that of a WE1S Virtual Workspace `Project`, so much so that there may well be value to developing the WE1S manifest spec in a way that is compatible with the Frictionless Data spec, or even to make it an extension of the Frictionless Data spec. This might well make the system more robust and more likely to be adopted by users outside the WE1S project. It would also be an early way to fulfill our promise in the grant proposal to make our schema compatible with other open access/open provenance standards.

There is already a high degree of compatibility between the WE1S manifest specifications and the Frictionless data specifications. For the most part, the changes would involve changes in the names of properties. In a few cases, decisions would have to be made about naming or formatting conventions where one spec or the other is stricter. The discussion below highlights individual issues I have identified.

<p style="color:red;font-weight:bold;">Warning! This is where things get a bit more technical.</p>

### The `_id` Property

The WE1S spec REQUIRES this property be present and RECOMMENDS that it be both human-readable and unique within the manifest's path. The use of the underscore is a concession to MongoDB, which REQUIRES the `_id` property as its primary key. MongoDB does not require the `_id` to be human-readable and allows auto-generated values or UUID (universally unique identifier) values. The closest Frictionless Data equivalent is `id`. It may be advisable to adopt one or other other and programmatically add or delete the underscore depending on whether the manifest is stored in the database. It may also be advisable to adopt greater enforcement of the uniqueness of the value, perhaps by adopting UUIDs. This would sacrifice human readability, but that function might be handled with the `name` property (see below).

Whilst Frictionless Data's `id` property _can_ be used for database keys, it can also be used for external identifiers, such as DOIs. So some recommendation should be made for distinguishing if and when `id` can have this function in the WE1S schema. It may be that WE1S properties like `refLocation` can be used for this purpose.

### The Frictionless Data `name` Property

The Frictionless Data `name` property contains a short url-usable (and preferably human-readable) name for a Data Package. It closely resembles the WE1S `id` property, except that it has some formatting restrictions: `name` values MUST be all lower case and contain only alphanumeric characters, ".", "-", and "_". It seems possible to adopt the `name` property to handle the "human-readable" recommendation of the current WE1S `_id` property, freeing up the `_id` property to have unique, but potentially non human-readable values. The main issues are whether the use of the keyword `name` will cause conflicts elsewhere in the schema (I believe not, at present) and whether we are OK with the formatting restrictions required by Frictionless Data.

### The Frictionless Data `description` Property

Frictionless Data REQUIRES that the value of the `description` property be formatted in Markdown and that the first paragraph be usable as summary information. Are we OK with adopting these specifications?

### The Frictionless Data `licenses` Property

Frictionless Data RECOMMENDS a `licences` property, which MUST contain an array of objects for each licence. Each object MUST contain a `name` property and/or a `path` property (pointing to the text of the licence). It MAY contain a `title` property (a human-readable title for the licence).

The WE1S equivalant is the `rights` property, which contains a simple prose statement of licensing rights or intellectual property restrictions. `Free culture` is assumed by default.

The Frictionless Data spec is a little more developed and seems useful to adopt for WE1S. We can maintain the default `free culture` value for `name`. The Frictionless data `path` property here differs from the WE1S global `path` property, which is assumed to be a MongoDB "materialized path", rather than a url. I am as yet not sure how to reconcile these.

### The Frictionless Data `profile` Property

In Frictionless Data, all content is either a `data-package` (the default), or a `data-resource`. Variants on the former included `tabular-data-package` and `fiscal-data-package`. The `data-resource` specification will be discussed below. Every project produced by the Virtual Workspace will be a Data Package and SHOULD therefore include the `profile` property to indicate this. It contains a url to the Data Package JSON Schema file. This file does not appear to contain a version number, so the version of the Data Package spec can be added with a `datapackage_version` property, if we feel we need this. However, as we are envisioning an extension of the Frictionless Data spec, we also need an indicator of the WE1S component. Probably the WE1S `namespace` property, REQUIRED in all manifests, is sufficient, but we may want to consider what it is called or even propose allowing an expansion of the values allowable for `profile` in the Frictionless Data schema.

### The Frictionless Data Data Resource Spec

A Frictionless Data `data-resource` is very much like a WE1S `collection` node. A comprehensive Data Resource example with all required, recommended and optional properties looks as follows.

```javascript
{
  "name": "solar-system",
  "path": "http://example.com/solar-system.csv", // Could also be a local or materialized path
  "title": "The Solar System",
  "description": "My favourite data about the solar system.",
  "format": "csv",
  "mediatype": "text/csv",
  "encoding": "utf-8",
  "bytes": 1,
  "hash": "",
  "schema": "",
  "sources": "",
  "licenses": ""
}
```

`mediatype` is equivalent to WE1S `mimeType`, and we could easily change the name. The `format`, `encoding`, `bytes`, and `hash` properties could easily be adopted by WE1S. `schema` probably falls under the same category. At present, Frictionless Data only has a schema for tabular data, which basically just describes the columns and rows in JSON format. For `sources`, see below.

Basically, a `data-resource` combines features of the WE1S `collection`, `RawData`, and individual data nodes. Since the only REQUIREMENT for a `data-resource` manifest is a path to the resource, this should not be a problem. The difficulty is that WE1S paths point upward in the hierarchy (e.g. `Corpus/collection/RawData`), whereas FrictionlessData paths point to the actual data file. I'm not sure how to reconcile this (and is it a problem elsewhere?).

### The Frictionless Data `sources` Property

The Frictionless Data `sources` property basically corresponds to a `Publications` node in the WE1S schema. The keyword `sources` may actually be a more flexible term, and it may be worth adopting for that reason.
