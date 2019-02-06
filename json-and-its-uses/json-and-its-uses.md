# JSON Format and its Uses in WE1S

## What is JSON?

JSON is an acronym for "JavaScript Object Notation", which refers to the way data objects are defined in the Javascript programming language. Although that tells you something about its origins, JSON format is often used independently of Javascript as a simple way to store data in plain text format. JSON format is relatively easy for humans to read but also capable of producing complex data structures which can be processed by computers.

WE1S stores data in JSON-formatted documents called "manifests". While much of the time you may create and edit manifests using out browser-based Workflow Management System, there may be times when you may need to work with them independently in a text editor like VS Code. Regardless, it is useful to have an understanding of how WE1S records its data. This document gives a quick introduction to JSON and its uses in the WE1S project.

## JSON Data types

JSON consists of five data types: numbers, strings (alphanumeric characters), Booleans (either `true` or `false`), objects (key-value pairs), and arrays (lists of numbers, strings, or objects). Arrays and objects can be nested to create complex data structures.

Each data type is identified by a particular format:

- `number`: Simply a number without quotation marks (e.g. `3`, `3.14`, etc.)
- `string`: A group of alphanumeric characters surrounded by double quotation marks (e.g. `"hello world"`)
- `Boolean`: Either the value `true` or `false` without quotation marks.
- `object`: A pair of curly brackets containing a key string and a value separated by a colon. An object can have multiple key-value pairs, separated by commas. E.g. `{"name": "John Smith", "age": 27}`.
- `array`: A pair of square brackets containing a comma-separated list of any data type. E.g. `[3, 3.14]`, `["George Washington", "Abraham Lincoln"]`, `[{"name": "George Washington", "age": 27}, {"name": "Abraham Lincoln", "age": 28}]`.

As far as computers are concerned, JSON data can be "serialized" as one long string of data, but the JSON format is typically indented in a way that makes it more human readable. Instructions for indenting JSON are provided below.

You may have already detected a possibly problem with the format. What if you need to record a string containing quotation marks? A value like `"this is a "string""` will be interpreted by the computer as ending at the second quotation mark. The way to get around this problem is to "escape" the quotation marks inside the string with a backslash like this: `"this is a \"string\""`.

## Editing JSON Documents

You can write JSON in any text editor. Since WE1S makes VS Code its standard editor, that will be used as the basis for the discussion here.

It is conventional to save JSON files with the extension `.json`. When you open a file with this extension, VS Code will automatically detect the format and provide some useful "syntax highlighting" to make the format more readable. If you are starting a new file, you can click `Plain Text` at the bottom right of the screen and select JSON as your language. This will provide syntax highlighting before you have saved the file. If you right-click and select `Format File`, VS Code will adjust the indentation to make your JSON formatting more readable.

As simple as JSON is, it is very easy to make mistakes by typos, missing commas, or improperly nested brackets. VS Code will often show you your errors with small curly red lines. You can also check that your JSON is valid by pasting it into [JSONLint](https://jsonlint.com/) online. This is a good practice before you save the file.

## WE1S Manifests and JSON Schema

Consider a JSON object like this: `{"GPA": 4.0}`. This is perfectly valid JSON, but the `GPA` keyword is unlikely to be found in a manifest for the WE1S project since student grades are the within the project's area of interest. Even if they were, we might want to store GPAs as string, rather than numbers. So we really need a _schema_ to tell us what keywords (also called "properties") can be in a manifest document and what data types they should have. By sticking to this schema, we can all write manifests that are consistent in their content and formatting.

For humans, the schema can be described in a user manual. The WE1S schema manual is available [here](https://github.com/whatevery1says/manifest/blob/master/we1s-manifest-schema-2.0.md). However, although the WE1S schema is fairly simple, it's still a lot of documentation to wade through, and you can make mistakes. So we generally use an automated process to validate your JSON documents against a version of the schema which is recorded in JSON Schema format. [JSON Schema](http://json-schema.org/) is a method of describing a schema entirely in JSON notation. You probably don't need to know the details of JSON Schema, but you can see our validation file for `collection` manifests [here](https://github.com/whatevery1says/manifest/blob/master/schema/v2.0/Corpus/collection.json), if you are interested. Basically, this is simply a set of rule for making sure that your JSON document conforms to the guidelines described in the documentation.

Here is an example of a `collection` manifest:

```javascript
{
    "name": "new_york_times",
    "title": "The New York Times",
    "namespace": "we1sv2.0",
    "metapath": "Corpus,new_york_times",
    "created": "2018-01-01",
    "sources": [{
        "title": "The New York Times",
        "path": "Sources,new_york_times"
    }],
    "contributors": [{
        "title": "Scott Kleinman",
        "role": "wrangler"
    }],
    "queryTerms": ["humanities"]
}
```

This manifest describes a collection called `new_york_times` using version 2.0 of the manifest schema. It outlines where the collection is stored (the `metapath`), when it was created, its source material, and contributors. The schema allows for a variety of optional properties, of which only `queryTerms` is used here. It indicates that the data in the collection contains the term "humanities".

When you create manifests in the Workflow management system, the values you enter in the web-based form are converted into a JSON format like this before they are stored in the database. You can then search the data by any of (or any combination of) the keywords in the data manifests.

## Writing Manifests in YAML

You don't _have_ to use JSON for a WE1S manifest. Technically, you just need to write something that has all the information required by the schema. But writing out this information in prose would make it unusable for the kind of searching mentioned above. This is why WE1S uses the JSON format. Nevertheless, writing JSON by hand can be tedious and error prone. One way around this is to employ the YAML format for writing and then convert to JSON. Although it is unlikely that you'll be working with JSON extensively, it's nice to have this strategy, so we provide some brief guidance here.

YAML stands for "YAML Ain't Markup Language" and is generally described as a "superset of JSON". Essentially, this means that it *is* JSON with a few extra features and that valid JSON is also valid YAML. But YAML allows some formatting that is a bit more human readable. Here is an example of the manifest above written in YAML:

```yaml
---
name: new_york_times
title: The New York Times
namespace: we1sv2.0
metapath: Corpus,new_york_times
created: '2018-01-01'
sources:
- title: The New York Times
  path: Sources,new_york_times
contributors:
- title: Scott Kleinman
  role: wrangler
queryTerms:
- humanities
```

That's arguably a lot easier to read. There are various online tools for converting from [JSON to YAML](https://www.json2yaml.com/) and [YAML to JSON](https://www.json2yaml.com/convert-yaml-to-json) (the links here will get you started). You can also set VS Code to YAML format. YAML files are generally saved with the extension `.yml` or `.yaml`.