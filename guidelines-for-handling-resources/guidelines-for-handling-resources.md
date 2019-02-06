# Guidelines for Handling Resources

## Table of Contents

* [Defintion of a Resource](#_definition-of-a-resource)
* [Web Content](#_web-content)
  * [Blog Posts](#_blog-posts)
  * [Website Pages](#_website-pages)
* [Other Resources](#_other-resources)
* [Storage of Resources](#_storage-of-resources)

## <a id="_definition-of-a-resource" name="_definition-of-a-resource">Definition of a Resource</a>

Documents produced by the WE1S project (other than those used in text mining and analysis) consist of web content (blog posts and some web page content) or "resources". Any document that we wish to archive on GitHub is considered a "resource". This applies in the following situations:

* It is desireable to implement version control on the document.
* The document is written in Markdown and we wish to display it directly in a website page and/or on GitHub.
* The document is in a format that is not intended to be converted to HTML (e.g. Word, PDF), and we wish to provide a link to it on the website.
* The document is intended for internal use and we wish to distribute it to project staff via GitHub.

## <a id="__web-content" name="__web-content">Web Content</a>

### <a id="_blog-posts" name="_blog-posts">Blog Posts</a>

Blog posts are generally not generally considered "resources", and we can leave their archiving to the Wordpress database. In general, however, they should be authored offline in Markdown and the Markdown text should then be pasted into the Wordpress text editor. The Jetpack plugin will convert the Markdown to HTML and save the Markdown to the database's `filtered_content` column, from which it can be extracted easily. This procedure has the additional advantage of using Markdown to enforce simple, consistent formatting.

The [StackEdit](https://stackedit.io/) editor is probably the most accessible online Markdown editor. The Markdown text can be copied from there directly into the Wordpress text editor. (Eventually, StackEdit will probably have the ability to publish directly to Wordpress, but it is not there yet.) More advanced users should be encouraged to author text in a code editor that employs linting (see below under **[How to Work with Markdown > Advanced Usage](https://github.com/whatevery1says/resources/blob/master/how-to-work-with-markdown/how-to-work-with-markdown.md#advanced-usage)**).

### <a id="_website-pages" name="_website-pages">Website Pages</a>

Like blog posts, some page material on the website may not be appropriate to archive as a "resource". In this case, the instructions for blog posts should be followed. Otherwise, the conent should be authored in Markdown using [StackEdit](https://stackedit.io/) or a code editor. This will encourage simple, consistent formatting and make it easy to convert the text to other formats.  More advanced users should be encouraged to author text in a code editor that employs linting (see below under **[How to Work with Markdown > Advanced Usage](https://github.com/whatevery1says/resources/blob/master/how-to-work-with-markdown/how-to-work-with-markdown.md#advanced-usage)**).

For material intended only for the website, the content can be pasted directly into the Wordpress text editor. However, most resources should be archived on GitHub. The best workflow will be to push the content to GitHub and then copy and paste the Markdown from there. It is possible to sync Wordpress and GitHub content, but the process is clunky and may not be worth it at this stage. If material published to the web is updated on GitHub, it should be part of the workflow to paste the new content into Wordpress and update the Wordpress page.

Non-textual assets (e.g. images) should be saved separately and archived on GitHub. The urls used to embed these assets in the web pages should be to the files archived on GitHub, not to the Wordpress media library.

## <a id="_other-resources" name="_other-resources">Other Resources</a>

Documents in formats other than Markdown or HTML should be archived on GitHub. In general, the "Markdown first" philosophy should be followed. That is, wherever possible, documents should be authored first in Markdown and then converted to other formats. This will encourage simple, consistent formatting, and make it easy to convert the text to other formats.

Conversion to Markdown to Word can be done by hand, but [Pandoc](http://pandoc.org/) does a very good job of automating the process. To use pandoc, install it and open a command line. Navigate to the folder containing the Markdown document and type `pandoc -s -o mydoc.docx mydoc.md`. This will create a new file called `mydoc.docx` baded on `mydoc.md`. The resulting Word document may need some hand editing, especially to introduce appropriate page breaks. This is an important step before converting to PDF format, which can be done using Word's `Save As` function.

Images can be embedded in Word and PDF files, but the originals should also be archived on GitHub.

In general, the Word files used to generate PDFs should be saved as "drafts". Minor changes to the formatting can then be made to the Word file and new PDFs generated. If the Word file is based on an original Markdown file, care should be taken to ensure that all changes to the text are made in both files. If there are drastic changes, only the Markdown should be edited, and the Word file should be regenerated based on the new copy.

## <a id="_storage-of-resources" name="_storage-of-resources">Storage of Resources</a>

All resources other than blog posts and some web content should be stored in the GitHub `whatevery1says` repo. Currently, WE1S maintains two repos, one for `research` and one for `resources`. These correspond to the menu items on the WE1S website. Drafts and items for internal use only should be place in the parallel `dev_research` and `dev_resources` repos. (It is recommended that Word files used to generate PDFs be stored in the two development repos.) No other categories are prescribed at this time.

Within the two main repos, each item should take the form of a [Frictionless Data](http://frictionlessdata.io/) data package. This consists of a JSON metadata file, the actual document, and a folder containing assets (e.g. images). The package may also contain a folder for versions in other formats, such as PDF. A typical file structure for each repo might therefore look like the following (which shows a `reports` subfolder in `research`:

```markdown
research
│   README.md
└───reports
│   |   README.md
│   │
│   └───report1
│   │   │   datapackage.json
│   │   │   report1.md
│   │   └───assets
│   │   │   image.md
│   │   └───pdf
│   │       report1.pdf
│   └───report2
│   │   │   datapackage.json
│   │   │   report2.md
│   │   └───assets
│   │       image.md
│   └─── ...
│
resources
│   README.md
└───resource1
│   │   datapackage.json
│   │   resource1.md
│   └───assets
│       image.md
│   │   datapackage.json
│   │   resource2.md
│   └───assets
│       image.md
└─── ...
```

The basic `datapackage.json` file should look like the following:

```javascript
{
  "name": "a-unique-human-readable-and-url-usable-identifier",
  "title": "A nice title",
  "resources": [{
      "path": "relative-path-to-file", // e.g. report1.md
    },{
      "path": "relative-path-to-asset-file", // e.g. assets/image.png
    },{
      "path": "relative-path-to-other-version-file", // e.g. pdf/report1.pdf
    }]
}
```

The value of the `name` property should be the same as the container folder. Be sure not to confuse the Frictionless Data `resources` property with the WE1S `resources` repo. Values for the `resources` property should be paths to assets or different versions of the document. Other metadata allowable in the [Frictionless Data spec](https://specs.frictionlessdata.io/data-package/) may be included but is not required by WE1S.
