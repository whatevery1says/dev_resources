# How to Work with Markdown

## Table of Contents

* [Introduction](#_introduction)
* [How to Write Markdown](#_how-to-write-markdown)
  * [Online Editors](#_online-editors)
  * [Code Editors](#_code-editors)
  * [Microsoft Word](#_microsoft-word)
* [Markdown on the WE1S Website](#_markdown-on-the-we1s-website)
* [Markdown on GitHub](#_markdown-on-github)
* [Handling Images](#_handling-images)
* [Inline HTML](#_inline-html)
* [Converting Other Formats to Markdown](#_converting-other-formats-to-markdown)
* [Further Suggestions for Moving from Word to Markdown](#_further-suggestions-for-moving-from-word-to-markdown)
  * [Advice for Authoring Documents in Microsoft Word](#_advice-for-authoring-documents-in-microsoft-word)
  * [Automated Word to Markdown Conversion](#_automated-word-to-markdown-conversion)
* [Advanced Usage](#_advanced-usage)
  * [Markdown Linting and Inline HTML](#_markdown-linting-and-inline-html)
  * [Source Control](#_source-control)
    * [VS Code](#_vs-code)
    * [Atom](#_atom)

## <a id="_introduction" name="_introduction">Introduction</a>

Markdown is a lightweight text markup system that uses punctuation marks to indicate formatting instructions. It is human-readable but also easy to convert to other formats, most commonly HTML. It is also _very_ easy to learn because it is simple and straightforward. Markdown allows only a limited number of styling possibilities, which ensures that text written in Markdown is consistent and easy to convert. Writing in Markdown is a good idea because it forces you to keep your formatting simple. You can author Markdown documents in a simple text editor.

It is highly recommended that you adope a "Markdown first" philosophy whenever possible. That is, author documents in Markdown and then convert to other formats. Converting documents from other formats _to_ Markdown is more complicated than converting documents _from_ Markdown. It is hard to automate because it generally involves eliminating complex and inconsistent formatting. It works best if the original document was produced using only styling and layout features that are allowable in Markdown. This is actually good practice for writing. Keep your text simple and streamlined without a lot of extra formatting. For instance, if you are using Word to write a document, be aware that tabs, centering, and multiple spaces are not allowable in Markdown. Markdown also provides a system of hierarchical semantic headings. Word does too (you can find them in *Styles* section in the Toolbar), but few people use them. This is a practice you should cultivate instead of formatting headings in bold, italics, or larger fonts. Let Word's built-in styles handle this (Word also allows you to create custom styles).

## <a id="_how-to-write-markdown" name="_how-to-write-markdown">How to Write Markdown</a>

It is conventional to save files written in Markdown with the extension `.md`. Most editors will recognize these files as Markdown and will highlight the formatting to make the text more readable.

There are _many_ options for writing Markdown. A good place to start is simply by learning Markdown from a cheat sheet. The following websites are extremely useful.

* [https://daringfireball.net/projects/markdown/syntax](https://daringfireball.net/projects/markdown/syntax)
* [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [https://en.wikipedia.org/wiki/Markdown](https://en.wikipedia.org/wiki/Markdown)

**Note that there are several dialects of Markdown. Wherever possible, care should be taken that Markdown conforms to the rendering requirements of the [GitHub-Flavored Markdown spec](https://github.github.com/gfm/). so that it renders nicely on the GitHub website.**

### <a id="_online-editors" name="_online-editors">Online Editors</a>

There are numerous WYSIWYG Markdown editors online, and you should experiment with them to get a feel for how Markdown renders as HTML. One of the best is [StackEdit](https://stackedit.io/). This allows you to edit Markdown with a side-by-side preview of the text rendered in HTML that changes in real time.

**Note: Most online editors do not enforce GitHub-Flavored Markdown standards. As a result, text that displays correctly in the online editor may not do so on GitHub. The differences are minor and generally easily corrected. For instance, the Markdown `#Heading1` will display as HTML `<h1>Heading1</h1>` in StackEdit, but not on GitHub.**

### <a id="_code-editors" name="_code-editors">Code Editors</a>

You can also use a code editor to write Markdown offline. Based on the usage of WE1S's project directors, the recommended code editors for use on the project are [VS Code](https://code.visualstudio.com/download) and [Atom](https://atom.io/).  See the section on **Advanced Usage** for further information on setting up a code editor for editing in Markdown.

### <a id="_microsoft-word" name="_microsoft-word">Microsoft Word</a>

It is possible, but not recommended, to edit Markdown files in Microsoft Word. If you do, make sure you save the file as plain text with the `.md` extension and watch for errors introduced by Word's autocorrect function. For Windows, there is a plugin called [Writage](http://www.writage.com/) that allows you to write Markdown directly in Word.

## <a id="_markdown-on-the-we1s-website" name="_markdown-on-the-we1s-website">Markdown on the WE1S Website</a>

The WE1S website uses the Jetpack plugin to handle text written in Markdown. You can write your pages and posts directly in Markdown format in the web editor. Wordpress will automatically convert it to HTML when you save, and the HTML is displayed on the public website. Wordpress stores both the rendered HTML and the original Markdown (in the `filtered_content` column of the database table). It is recommended that you author your text in a code editor or an online Markdown editor similar to [StackEdit](https://stackedit.io/) and then paste the Markdown into the Wordpress code editor. For further information, see the [Guidelines for Handling Resources](https://github.com/whatevery1says/resources/blob/master/guidelines-for-handling-resources/guidelines-for-handling-resources.md).

## <a id="_markdown-on-github" name="_markdown-on-github">Markdown on GitHub</a>

GitHub is a cloud-based service that provides repositories for code and documents. It also provides a wiki and discussion forum (called "Issues") for each repository. Any Markdown document deposited in GitHub is automatically rendered in beautiful HTML on the GitHub website. The [document you are reading](https://github.com/whatevery1says/resources/blob/master/how-to-work-with-markdown/how-to-work-with-markdown.md) is an example. If you wish to see the original Markdown, you can click the [`Raw`](https://github.com/whatevery1says/resources/raw/master/how-to-work-with-markdown/how-to-work-with-markdown.md) button available on any GitHub page.

GitHub uses the `git` version control system to keep track of changes made to files. This is not the place for a full git/GitHub tutorial, but the basic workflow is follows:

1. Create and publish a new repository on GitHub **or** if the repository already exists on GitHub, "clone" it to make a _local_ copy on your computer.
1. If you have a cloned repository, "pull" the latest version in case someone else on the team has made modifications.
1. Create or edit files in your cloned repository.
1. "Commit" the changes. This "stages" the changes for merging with the _remote_ copy on GitHub.
1. "Push" the commit to the remote repository on GitHub.

Steps 1, 2, 4, and 5 can all be accomplished using `git` from the command line, but this has a learning curve. An easier approach is to download the [GitHub desktop client](https://desktop.github.com/). Also, many code editors allow you to execute `git` commands from within the editor. See the section on **Advanced Usage** for further details.

For a full tutorial on getting up and running with GitHub aimed at digital humanists, see the Programming Historian's [An Introduction to Version Control Using GitHub Desktop](https://programminghistorian.org/lessons/getting-started-with-github-desktop).

For further information on the place of GitHub in the WE1S workflow, see the [Guidelines for Handling Resources](https://github.com/whatevery1says/resources/blob/master/guidelines-for-handling-resources/guidelines-for-handling-resources.md).

## <a id="_handling-images" name="_handling-images">Handling Images</a>

The following format is used to embed images in a Markdown document.

```markdown
![GitHub Logo](/images/logo.png)
```

This will be rendered in HTML as

```html
<img src="/images/logo.png" alt="GitHub Logo">
```

Note that the image file in the link must be placed in the appropriate location on GitHub or uploaded to the Wordpress media library.

## <a id="_inline-hitml" name="_inline-html">Inline HTML</a>

Most Markown documents are destined to be rendered as HTML, either on the WE1S website or on GitHub. In both cases, additional formatting can be added to a Markdown documents using "inline HTML". In other words, HTML codes can be entered directly in the Markdown. Here is an example:

```markdown
[This is a link](mylink.html) in Markdown and <a href="my link.html" target="_blank">this is a link in HTML</a>.
```

In both cases, the result will render as a link. However, using HTML in the second case allows you to cause the link to open in the page in a new tab, something that is not possible in Markdown.

GitHub-flavored Markdown cannot handle footnotes, so inline HTML provides a workaround. The structure should look something like this:

```markdown
<a name="_ftn1">This is the main text.[<sup>1</sup>](#ftn1)

***

Footnotes:

<a name="ftn1">[<sup>1</sup>](#_ftn1) This is a footnote.
```

The HTML `<a>` tag provides anchors for the footnote and the referring text. The footnote number is a link to the appropriate anchor.

## <a id="_converting-other-formats-to-markdown" name="_converting-other-formats-to-markdown">Converting Other Formats to Markdown</a>

In general, the "Markdown first" philosophy should be followed, but in some cases, documents in Word or HTML format may need to be converted to Markdown, especially for display as web pages or on GitHub. This guide provides practical advice on how to use Markdown, convert between formats, and move documents in and out of a GitHub repository.

Here are some websites for converting from other formats:

* [Word-to-Markdown](https://word-to-markdown.herokuapp.com/)
* [HTML-to-Markdown](https://domchristie.github.io/to-markdown/)
* [Pandoc](https://pandoc.org/try/)

Note that these sites will be more successful if the formatting of the original Word or HTML document is consistent and contains only formatting allowable in Markdown. You may have to hand edit the results afterwards.

## <a id="_further-suggestions-for-moving-from-word-to-markdown" name="_further-suggestions-for-moving-from-word-to-markdown">Further Suggestions for Moving from Word to Markdown</a>

### <a id="_advice-for-authoring-documents-in-microsoft-word" name="_advice-for-authoring-documents-in-microsoft-word">Advice for Authoring Documents in Microsoft Word</a>

1. When authoring in Microsoft Word, restrict formatting to the following:

* Headings 1-5
* Emphasis (italics)
* Strong emphasis (bold)
* Strikethrough

1. Do use different fonts or font sizes, except if they are changed by Word's heading styles.
1. Do not centre, indent, or justify. Any horizontal spacing should be created by Word's heading, list, or table functions.
1. Make sure you use Word's bullet and numbering list functions.
1. Keep tables very small and simple.
1. Use as few images as possible.
1. Avoid the use of footnotes.

The last two require some explanation. It is possible to attach images to a Markdown file, but in converting from Word, they will be lost. So images will have to be added after conversion. Although some dialects of Markdown support footnotes, GitHub-flavored Markdown does not. There is a workaround using inline HTML, but it also generally needs to be implemented after the document is converted.

### <a id="_automated-word-to-markdown-conversion" name="_automated-word-to-markdown-conversion">Automated Word to Markdown Conversion</a>

Save the Word file and then use an automated method to convert it to Markdown, such as [Word-to-Markdown](https://word-to-markdown.herokuapp.com/) or the [Writage](http://www.writage.com/) plugin for Word (Windows only). You can, of course, save the file as plain text and then change the extension to `.md`. Any way you do it, you will probably have to double check the results to make sure the Markdown is correct. You can do this using [StackEdit](https://stackedit.io/) or a code editor with Markdown preview.

Note that images must be kept as separate files with links to them in the Markdown document. An image looks like this:

```Markdown
![My Logo](https://github.com/.../common/images/icon48.png "Logo Title Text")
```

This will be rendered as

```HTML
<img src="https://github.com/.../common/images/icon48.png" alt="My Logo" title="Logo Title Text">
```

Word probably does not supply values for `alt` and `title`, so you will need to add them. The `alt` text displays if the image link is broken, and the `title` text displays in a tooltip when you run your browser over the image. It is good web practice to provide values for `alt` and `title`, especially the former.

Tables in Word are also probably not likely to convert exactly as you want them. You may have to redesign them in Markdown. The [Markdown Table Generator](https://www.tablesgenerator.com/markdown_tables) tool can be helpful for this process.

When you are done with the conversion, save the new file with the `.md` extension.

## <a id="_advanced-usage" name="_advanced-usage">Advanced Usage</a>

Based on the usage of WE1S's project directors, the recommended code editors for use on the project are [VS Code](https://code.visualstudio.com/download) and [Atom](https://atom.io/). In addition to enabling offline editing, code editors allow you to take advantage of other advanced features such as linting and source control.

### <a id="_markdown-linting-and-inline-html" name="_markdown-linting-and-inline-html">Markdown Linting and Inline HTML</a>

In order to ensure that Markdown renders correctly on GitHub, care should be taken that Markdown conforms to the rendering requirements of the [GitHub-Flavored Markdown spec](https://github.github.com/gfm/). This is a stricter standard than most web-based Markdown editors employ. For instance, the Markdown `#Heading1` will display as HTML `<h1>Heading1</h1>` in StackEdit, but not on GitHub. The most fool-proof method of doing this is to author Markdown in a code editor with "linting". "Linting" is a method of showing errors in code. Markdown linters will display errors where the markup does not conform to strict standards. They also provide guidance for how to correct the error.

Instructions for setting up Markdown linting in your editor of choice are easily found in online tutorials. Here are some links to get you started:

* VS Code supports Markdown files out of the box. You just start writing Markdown text, save the file with the `.md` extension. You can switch between Markdown and Preview mode with `Ctrl+Shift+V`, and you can view the preview side-by-side  with `Ctrl+K V`. For more information, see [Markdown and VS Code](https://code.visualstudio.com/docs/languages/markdown).
* To install a Markdown linter in VS Code, select `View > Extensions` and enter `markdownlint` in the search field. When it comes up, click `Install` and then `Reload` when installation is complete.
* **We need some instructions for Atom.**

Most linters will enforce a rule that a Markdown document cannot contain inline HTML. For instance, GitHub-Flavored Markdown does not have a method of opening a link in a new tab. Hence, it is legitimate to replace a standard Markdown link like `[My Link](url)` with `<a href="url" target="_blank">My Link</a>`. In other cases, such as internal links for footnotes or special formatting, it may be useful to simply use HTML markup directly within the Markdown document (inline HTML). Since the Markdown will be converted to HTML anyway on GitHub and the WE1S website, this is allowable. Therefore, users of Markdown linters may ignore the "no inline HTML" rule.

### <a id="_source-control" name="_source-control">Source Control</a>

If you are using a code editor to write your Markdown (because you want the linting) the next step is to push the text directly to GitHub. Most modern code editors can do this, either natively or with extensions. This has the added advantage that you can pull the document from GitHub directly into your editor, make changes, and then push them without ever leaving your editor. Here are some instructions for doing this is popular code editors.

To use source control, you must first clone the GitHub repo onto your local machine.

#### <a id="_vs-code" name="_vs-code">VS Code</a>

Open a file in your local repo. In the `View` menu, select `SCM` (Source Control Manager). You should see the repo listed, along with the file you have open. Click the three dots at the top and select `Pull` to pull the latest version of the file.

Next, make some changes to the file and save. The files should now have an `M` next to it for "modified". Click the plus icon to stage the file. In the `Message` field, type a description of the commit and click the check mark to commit it. You are now ready to push your changes to the repo. Click the three dots again and select `Push`.

The Source Control Manager allows you to do lots of other fancy things with `git`, but this procedure captures most workflows.

#### <a id="_atom" name="_atom">Atom</a>

**We need some instructions for Atom.**