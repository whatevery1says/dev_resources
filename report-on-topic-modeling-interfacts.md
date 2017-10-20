# Topic Modeling Systems and Interfaces

The 4Humanities "WhatEvery1Says" project conducted a comparative analysis in 2016 of the following topic modeling systems/interfaces. As a result, it chose to implement Andrew Goldstone's DFR-browser for its own work.

Last revised November 12, 2016.

## Table of Contents

* [ConVisit](#convisit)
* [DFR-Browser](#dfr-browser)
* [InPHO Topic Explorer](#inpho)
* [The Networked Corpus](#networked-corpus)
* [pyLDAvis](#pyldavis)
* [Serendip](#serendip)
* [Termite](#termite)
* [TIARA](#tiara)
* [TOM](#tom)
* [TOME](#tome)
* [The Topic Browser](#topic-browser)
* [Topical Guide](#topical-guide)
* [TopicNets](#topicnets)
* [TWIC](#twic)

(These following were the materials that the WE1S team researchedin advance of its February 18, 2016, meeting focused on choosing and implementing a system/platform/interface for the exploration and interpretation of topic models.)

***

## <a name="convisit">ConVisIT</a>

* **Description**: E. Hoque and Giuseppe Carenini (2015), ["ConVisIT: Interactive Topic Modeling for Exploring Asynchronous Online Conversations"](http://www.cs.ubc.ca/~carenini/TEACHING/CPSC503-16/READINGS/iui0167-paper-SUBMITTED.pdf)
* **Topic modeling workflow**:
  * An all-in-one, start-to-finish system that does its own topic modeling of a corpus.
* **Notable interpretive features of interface**:
1. Interactive visualization interface designed for topic modeling asynchronous conversation on the Internet (email, blog comments, etc.).
1. Interface shows overall conversation (left panel in figure)
1. Interface also shows the actual conversation (right panel in figure)
1. "Human-in-the-loop" feature to allow humans iteratively to assess results of a topic model and tweak it interactively in a sense-making activity--e.g., change granularity of topics, merge or split topics, suppress a topic, specify that words must (or must not) be in a topic,
1. Has an algorithm for automatic labeling of topics. (p. 4 of PDF)
1. Feedback on the interface was assessed through a user study.
* **Code site**: [unknown]
* **Notes by WE1S team**:
  * _Alan_: Can it be adapted for articles?

### Screen Shots

[![ConVisIT](http://4humwhatevery1says.pbworks.com/f/1454822801/ConVisIT-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940468/ConVisIT.jpg)

***

## <a name="dfr-browser">DFR-Browser</a>

* **Description**: Andrew Goldstone, ["Dfr-Browser: Take a MALLET to Disciplinary History"](http://agoldst.github.io/dfr-browser/) (2013)
* **Demos**: [Topics in](http://agoldst.github.io/dfr-browser/demo/) _[PMLA](http://agoldst.github.io/dfr-browser/demo/)_ | [Topics in](http://signsat40.signsjournal.org/topic-model/) _[Signs](http://signsat40.signsjournal.org/topic-model/)_ | [Hathi Trust Fiction 1920-22](http://jgoodwin.net/htb/)
* **Topic modeling workflow**:
  * Out of the box, Goldstone's DFR-Browser is specialized to take input from Jstor's [DFR (Data for Research)](http://about.jstor.org/service/data-for-research) service, run it through Mallet using Goldstone's companion R package, [dfrtopics](http://github.com/agoldst/dfrtopics), and then use _d3_ to generate a dynamic visual exploration interface. This start-to-finish workflow is modularized, however, allow for the use of alternative methods for generating the topic models and formatted data files that DFR-Browser expects:
  * Instead of using Goldstone's R package to generate the Mallet topic model and then create the specially formatted data files for the DFR-Browser, a user can run Mallet and output the formattted data files entirely on the command line. (See [instructions here](https://github.com/agoldst/dfr-browser#preparing-data-files-entirely-on-the-command-line) in the Github repo.)
  * There is also a section in the Github repo titled ["Browser data file specifications"](https://github.com/agoldst/dfr-browser#browser-data-file-specifications) that gives detailed instructions about the format and nature of the data files that DFR-Browser expects. (In principle, this should allow topic model files that were pre-generated in other ways to be converted into data files for DFR-Browser.)
* **Notable interpretive features of interface**: A dynamic visual exploration interface with several main views:
  * _"Overview"_ (top figure at right) showing topics as circles laid out in a regular grid, each circle labeled with the six most important words in a topic. Clicking on a topic brings the user to →
  * _"Topic" view_ (bottom figure at right) showing a ranked list of words in the topic with bars representing relative weight (left panel), a timeline graph of the topic's weight in the corpus, and a list of articles ranked by the amount of the topic infused in them.
  * Clicking on a word in the ranked list of topic words brings the user to → _"Word" view_, which shows what other topics the word appears in (and its relative weight in that topic).
  * Clicking on a document brings the user to → _"Document" view_, which shows a ranked list of other topics in that document (and their relative weights in the document)
  * Clicking on a bar in the timeline graph of a topic brings the user to → a view showing the top documents in that year infused by that topic.
* **Code site**: [GitHub repo](https://github.com/agoldst/dfr-browser). The following sections of the documentation on Github indicate that we might be able to generate the topic-modeling and other data files for the DFR-Browser with the WE1S material:
  * ["Preparing data files entirely on the command line"](https://github.com/agoldst/dfr-browser#preparing-data-files-entirely-on-the-command-line)
  * ["Adapting this project to other kinds of documents"](https://github.com/agoldst/dfr-browser#adapting-this-project-to-other-kinds-of-documents)
* **Notes by WE1S team**:
  * _Alan_: we should try using the command line as instructed in the documentation to see if we can create the data files in the format needed for DFR-Browser
  * _Lindsay_: I kind of got this to work. With Goldstone's new instructions and the prepare-data python script, I was able to figure out how to get the data into the format the browser needs in the command line. I was also able to do this using the dfrtopics package in R with a pre-run mallet file (which I did in the command line). However, I haven't yet figured out how to properly configure the browser's main js file so that it will all display properly (right now only the overview view works as it should). Also, I tried this on a very small subset of our corpus (10 articles from the NYT) because getting the metadata into the right shape so that dfrtopics/the prepare-data python script can read it properly is still something I don't know how to do. I just did it manually, and it worked, but we would have to create a script that could wrangle metadata for us in order to do this for a larger number of documents.

### Screen Shots

[![DFR-Browser, multiple topics view](http://4humwhatevery1says.pbworks.com/f/1454822812/dfr-browser-1-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940474/dfr-browser-1.jpg)[![DFR-Browser, single topic view](http://4humwhatevery1says.pbworks.com/f/1454822813/dfr-browser-2-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940480/dfr-browser-2.jpg)

***

## <a name="inpho">InPhO Topic Explorer</a>

* **Description (Demos)**: [home page](http://inphodata.cogs.indiana.edu/)
* See also Jaimie Murdock and Colin Allen (2015), ["Visualization Techniques for Topic Model Checking"](http://www.aaai.org/ocs/index.php/AAAI/AAAI15/paper/viewFile/10007/9852)
* **Topic modeling workflow**:
  * An all-in-one, start-to-finish system; does its own topic modeling of a corpus.
* **Notable interpretive features of interface**:
  * Interactive visual exploration interface that shows:
  * List of all documents in a corpus (file names listed vertically down the left, with the first line of the document showing to help the user grok the article). Documents are ranked according to the weight of the topic that is a user's "focus" at present. (E.g., if a user is examining Topic 1, then the document where Topic 1 is most prevalent will be at the top.)
  * Bands of color superimposed over every document filename and first line that are color-coded to the topics in the topic model (where the legend for topic colors is at the right)
  * The relative size of each color band among all the colors in a document indicates the weight of specific topics in the article.
  * The cumulative width of the color bands for a document indicates the similarity of the document to the user's current "focus" topic (or document).
  * Clicking on a color anywhere reset's the "focus" to the topic corresponding to that color, with the whole list of articles and color bands shifting to reorient around that topic (ranked with the articles most expressive of that topic at the top).
  * When a topic is selected, clicking the "Top Documents for [Topic]" button at lower right of the interface "will take you to a new page showing the most similar documents to that topic's word distribution."
  * There is a search function to identify which documents in a corpus contain a word.
* **Code site**: [GitHub repo](https://github.com/inpho/topic-explorer) (an Anaconda 2.7 Python distribution)
* **Notes by WE1S team**:
  * _Alan_: This is a package for Python 2.7\. I tried to install, but installation of the underlying VSM module failed. One issue that appeared in the error messages: "error: Microsoft Visual C++ 9.0 is required (Unable to find vcvarsall.bat). Get it from [http://aka.ms/vcpython27](http://aka.ms/vcpython27)"  I've seen this error before when a package installation on a Windows machines calls on Visual C++ as its compiler, but the particular machine does not have Visual C++.
  * Scott: The above issue has supposedly been addressed (as of May 25, 2016), so it might be worth pulling the repo again. The tool has some interesting features that might help in defining stopword lists.

### Screen Shots

[![InPhO](http://4humwhatevery1says.pbworks.com/f/1454823924/inpho-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940711/inpho.jpg)

***

## <a name="networked-corpus">The Networked Corpus</a>

* **Description**: Jeff Binder and Collin Jennings, [The Networked Corpus](http://www.networkedcorpus.com/)
  * See also article: Jeffrey Binder and Collin Jennings (2014), ["Visibility and Meaning in Topic Models and 18th-Century Indexes"](http://llc.oxfordjournals.org/content/29/3/405.full) (2014)
* **Topic modeling workflow**: Takes input from Mallet.
* ** **Notable interpretive features of interface**:
  * Interactive visualization interface that takes input from Mallet. The key design principle of the interface is to avoid using topic labels (which can be deceptive) but instead to provide an easy way to identify passages in documents that are "dense" with a particular topic, allow them to be compared to other passages also dense with the topic, and thus provide the user with an understanding of a topic's meaning built up from intertextual context.
  In particular, the interface:
    * Shows a document in the left panel; and shows a list of topics (by number) in the right panel
    * Choosing a topic number highlights in the document the words that belong to that topic
    * A line graphs the topic "density" of passages in the document, with peaks indicated with asterisk. Clicking on the asterisk calls up a list of links to other passages (including in other documents) that are dense with that topic.
    > (The density functions in the interface are calculated using Mallet's topic-state file as follows: _"the density function is computed using kernel density estimation, which takes into account the words in nearby lines. Using these density functions, the program picks out ‘exemplary passages’ for each topic based on a simple rubric. Passages are only selected if the topic matches at least a certain number of words in the text (default 25), and they are only added if the topic’s maximum density in the text is at least (by default) four times as high as the average density of the whole document. If both of these conditions are met, an asterisk is created at the point of greatest density, with links to every other asterisk that was created for that topic."_)

 _Note_: one interesting theoretical tenet of The Networked Corpus is that topic modeling produces an apparatus for understanding texts and moving around them non-linearly in a way analogous to earlier "indexing" (and other such apparatus) in the history of writing and print.
* **Code site**: [GitHub repo](https://github.com/jeffbinder/networkedcorpus)
* **Notes by WE1S team**:
  * _Scott_: **[Instructions for implementing The Networked Corpus](https://github.com/scottkleinman/WE1S/tree/master/networkedcorpus)**.; includes adapted version of the code files as [zip file](https://raw.githubusercontent.com/scottkleinman/WE1S/master/networkedcorpus/networkedcorpus.zip); currently the instructions are for implementation on a Windows machine.
  * _Alan's_ **[step-by-step version of Scott's instructions](http://4humwhatevery1says.pbworks.com/f/w/page/106519659/Alan's%20Instructions%20for%20Implementing%20The%20Networked%20Corpus)**, including a temporary kludge solution for non-ASCII character problems (arrived at after debugging correspondence with Scott below).
  * _Alan_: This set of instructions gets The Networked Corpus to run. However, the results are not as expected and do not match the screenshots seen at the right. At first, my thought was that the _browser.css_ and _index.css_ files generated by the _gen-networked-corpus.py_ script, together with the HTML in the html versions of each original text file also generated by that script, need to be tweaked for today's browsers. However, after investigation and experiments, that seems not to be the case.
  Instead, the problem seems to lie in a mismatch between our input text format and that expected by Networked Corpus. Here are the relevant instructions in the Networked Corpus Github site: _"The text files must have hard line breaks at the end of each line. This is used to calculate how far down the page a word occurs, and also affects how wide the text will appear in the browser. If your source documents do not have line breaks and you are on a Mac or Linux system, you can use the 'fold' command to wrap them automatically. It doesn't matter whether the line breaks are Unix or DOS-style. Finally, the first line of each file should be a title; this will be used in the table of contents and in a few other places."_
  The plain-text article files in the WE1S corpus have no line breaks. Less important, they are not formatted in a way that makes the first line the title. (Instead, Networked Corpus ends up treating the entire text as a title, placing that in the title element in the head of each of the HTML file version it generates for an article.)
  When using Mallet to create a topic model, the format of the original plain-text file and the presence or absence of line breaks is irrelevant. However, the way Networked Corpus seems to work is that it creates a HTML version of each original plain text file, which when opened in a browser is correlated via javascript scripts to the Mallet data about that file on a token-by-token basis. The format of the original plain-text files and the presence or absence of line breaks has an impact on these HTML files and they way they are displayed in a browser. In particular, Networked Corpus creates in the HTML page for an article a table of the text in which topic words for a chosen topic are highlighted. Each "line" of a text is supposed to be a single row, so that the table extends down the page row-by-row. But if the original plain-text file has no line breaks, then there is just a single row extending off the right of the page, nullifying the whole point of Networked Corpus's document view of the topic model.
  It seem that the next step is to try the "fold" command referred to in the instructions from Networked Corpus's Github site above on the WE1S article files and see what we get.
* Debugging issues to date leading to above implementation solution:
* _Alan's error report_ in response to Scott's initial instructions for implementing The Networked Corpus. Implementation produced the following error:

```python
    ___init__.py", line 586, in <module>_
    _    from ._ufuncs import *_
    _ImportError: DLL load failed: The specified module could not be found._
```

* _Scott on the DLL load error_: "I think the answer might be [here](http://stackoverflow.com/questions/31596125/python-dll-load-failed). Try running `conda update scipy` from the command line."
* _Alan's error report_: "This worked.  I'm finally getting gen-networked-corpus.py to run.
However, I'm now getting a unicode error:

```python
      _File "C:\Users\Alan\Anaconda\lib\codecs.py", line 492, in read_
    _    newchars, decodedbytes = self.decode(data, self.errors)_
    _UnicodeDecodeError: 'utf8' codec can't decode byte 0xac in position 0: invalid start byte_
    I created the .mallet file for the Mallet topic model using the regex parameter you
     suggested: _--token-regex "[\p{L}\p{M}]+"_
```

    I'm guessing this is the kind of error that caused you to start debugging the unicode problems in the first place. Let me know if you have any suggestions."

* _Scott's response_: "The line causing the Unicode error is part of a loop through a directory file list, so it seems to run into problems if the directory contains something other than the text files you are using to generate your topic model, This includes the Mallet output. When I set line 303 to a directory containing only the text files (in this case, one of your early New York Times collections), I didn't get the error.

Unfortunately, I got another error at the next stage, where the script was getting hung up at the name "François". Obviously, we can avoid this problem by striping diacritics,but we shouldn't have to. When I get a chance, I'll try to figure it out. But go ahead and try the advice in the previous paragraph, and see if it works for you."

* _Alan's error report_: "Thanks, Scott. I see. I was misunderstanding what the "datadir=" in line 303 is supposed to point to: the directory of original text files and not the directory of Mallet output files for the topic model of those text files.

Unfortunately, after getting that right I am getting another Unicode error that may be indicating an unexpected character in the plain text (just as you did):

```python
      _File "C:\Users\Alan\Anaconda\lib\encodings\cp437.py", line 12, in encode_
    _    return codecs.charmap_encode(input,errors,encoding_map)_
    _UnicodeEncodeError: 'charmap' codec can't encode character u'\u0301' in position 72: character maps to <undefined>_
```

* _Alan's temporary kludge solution to the above error_: Use "search and replace" in Notepad++ (set to regex) to delete all non-ASCII characters in the article files being topic modeled for The Networked Corpus. ([See instructions](http://4humwhatevery1says.pbworks.com/f/w/page/106519659/Alan's%20Instructions%20for%20Implementing%20The%20Networked%20Corpus))
* (_Scott's earlier notes_: Some observations: The script must be run from within the input directory, and the script expects the Mallet output files to be named as shown in the sample command on GitHub. When I ran it, I encountered Unicode errors, so I tried a model using `<span style="font-family:'Courier New';">--token-regex '[\p{L}\p{M}]+'`, as suggested on the GitHub repo. However, this caused the Mallet train-topics command to fail. Apparently, in Windows the regular expression _must_ be enclosed in double quotes. The Python script also seems to have substantial problems with character encoding and/or Windows. I am hacking my way through it, gradually getting closer to a full implementation, but at the moment I'm stuck on a particularly confusing block of code. **Update**: I have never actually managed to get `<span style="font-family:'Courier New';">--token-regex` to work in Mallet, so the point about double quotes is important independent of the Networked Corpus tool. As for the tool itself, I have finally managed to get it to run all the way through. I had to hack the code and inject my own paths to get it to pull data from the right folders. The result was a little disappointing, as it produced buggy html/css/javascript (or some combination of those). The following information is readable. Document Index, Topic Index, top 10 topics in each document, top 10 documents in each topic. The script is supposed to choose "exemplary passages" if the topic matches 25 words in the text and the topic's maximum density in the text is at least 4 times as high as the average over the whole document. There did not appear to be any "exemplary passages", perhaps because I used Mallet's tiny sample data set to build my model. Supposedly, if both of these conditions are met, an asterisk is created at the point of greatest density, with links to every other asterisk that was created for that topic. From the images displayed on the website, this appears to be a visualisation function using protovis.js. Either the javascript failed or it wasn't called simply because my data did not produce any exemplary passages.)
* _Alan_: Just to add information that may, or may not. be relevant to Scott's original problem with Unicode issues as documented in his note: the WE1S scraping workflow saves all plain-text files in UTF-8.

### Screen Shots

[![Networked Corpus](http://4humwhatevery1says.pbworks.com/f/1454822821/networked-corpus-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940486/networked-corpus.jpg)
[![Networked Corpus](http://4humwhatevery1says.pbworks.com/f/1455229070/NetworkedCorpus1.PNG)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/105097671/NetworkedCorpus1.PNG)
[![Networked Corpus](http://4humwhatevery1says.pbworks.com/f/1455229070/NetworkedCorpus2.PNG)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/105097674/NetworkedCorpus2.PNG)
[Click for a readable image](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/105097674/NetworkedCorpus2.PNG)

***

## <a name="pyladavis">pyLDAvis</a>

* **Description**: Ben Mabey and Paul English, [pyLDAvis](https://github.com/bmabey/pyLDAvis)
* A Python port of the LDAvis R package.
* For a concise explanation of the visualization see this [vignette](http://cran.r-project.org/web/packages/LDAvis/vignettes/details.pdf) from the LDAvis R package.
* GitHub
* **Topic modeling workflow**:
  * Takes input from multiple types of topic models.
* **Notable interpretive features of interface**:
  * The GitHub site links to numerous examples and demos.
* **Notes by WE1S team**:
  * _Not yet reviewed._
  * Requires scikit-bio package, which is not yet supported for Windows. Windows support is scheduled for July 2016\. In the meantime, there may be a workaround [here](http://stackoverflow.com/questions/27029212/trouble-installing-scikit-bio-on-windows-xp), but it has not yet been tested.
  * Additionally, scikit-bio is now no longer compatible with Python 2 and thus would require a separate Python 3 virtual environment (although that's relatively easy to do in an Anaconda installation). It may be worth looking into using the [R package](https://github.com/cpsievert/LDAvis).

### Screen Shots

[![pyLDAvis](http://4humwhatevery1says.pbworks.com/f/1459712760/pyLDAvis1.png)](http://4humwhatevery1says.pbworks.com/f/w/file/106758792/pyLDAvis1.png)
[![pyLDAvis](http://4humwhatevery1says.pbworks.com/f/1459712811/pyLDAvis2.png)](http://4humwhatevery1says.pbworks.com/f/w/file/106758792/pyLDAvis2.png)

***

## <a name="serendip">Serendip</a>

_Note: Parts of the descriptions and screenshots in the mini-report on Serendip here are excerpted from Scott Kleinman's [report-on-serendip.pdf](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104432563/report-on-serendip.pdf). Other descriptions and one screenshot are based on the Eric Alexander et al. article._

* **Description**: Eric Alexander, et al. (2014), ["Serendip: Topic Model-Driven Visual Exploration of Text Corpora"](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiti_zIh7TKAhUBTGMKHTi_At0QFggiMAE&url=https%3A%2F%2Fgraphics.cs.wisc.edu%2FPapers%2F2014%2FAKVWG14%2FPreprint.pdf&usg=AFQjCNG-VY5ModzUaOQo8TrvVefKg50a5w&sig2=d-jzuGMxh9yFNjkrud5ghw) (preprint)
  * See also the [Project iPython notebook site](http://vep.cs.wisc.edu/serendip/).
* **Topic modeling workflow**:
  * Serendip runs in a Python-Flask environment. It comes with a separate command-line tool to call Mallet and generate topic models. The Mallet output data is deposited in a Corpora folder and can then be accessed by the Serendip interface. In addition to implementing Mallet, the command-line tool generates multiple files used by the interface to navigate and manipulate the data. Therefore, Serendip will not work if independently generated Mallet output files are deposited in the Corpora folder. It is possible that the script could be modified to read independently generated Mallet data, but this would require some hacking of the Python script.
* **Notable interpretive features of interface**:
  * Serendip is designed to give a view of a topic model at many scales, and with much connection between views. There are three main views (see 1st figure at right):
  * _CorpusViewer_: "At the corpus level, we provide a reorderable matrix to highlight adjacencies between documents and topics." This view shows "a re-orderable matrix that connects documents to topics. To address the “many documents” and “many topics” issues of scale, the matrix supports filtering and selection, aggregation, and ordering." "We provide a query-system that allows users to pick out documents and topics based on their metadata. Once selected, these sets can be hand-tuned, colored, moved to a more prominent position in the matrix (typically the top-left corner), used as a basis for reordering the matrix ... or saved to be explored later."
  * _TextViewer_: "At the document level, we use tagged text and overview displays to help readers find and analyze passages in large documents." This view shows a "tagged text visualization shows the topics and the text. To support long documents, a summary graph shows how the topics occur over the length of the document."
  * _RankViewer_: "Finally, at the level of individual words—a level we only observed the need for after watching users interact with our text level tool—we introduce a ranking visualization that shows how words are distributed across the topic." This view "allows users to examine specific words and see which topics use them. This tool is useful for relating topics and words, and comparing different topics and words. It can provide topics (and orderings of topics) to explore more closely in other views."
  * Serendip provides three metrics for ranking relationships between topics and documents:
  * Frequency (the percentage of a given topic accounted for each word) -- biased towards words appearing in many topics
  * Information Gain (the information words gain towards identifying a given topic) -- biased towards rare words that best distinguish topics
  * Saliency (frequency multiplied by information gain) -- finds salient words across an entire model, not just within a topic. Saliency is the default ranking metric.
* **Code site**: [Project iPython notebook site with download and use instructions](http://vep.cs.wisc.edu/serendip/). (Python 2.7)
* _Scott Kleinman's_ [report-on-serendip.pdf](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104432563/report-on-serendip.pdf)
* _Scott Kleinman's_ [Instructions for implementing Serendip](https://github.com/scottkleinman/WE1S/tree/master/serendip)

## Screen Shots

[![Serendip - three main views](http://4humwhatevery1says.pbworks.com/f/1454822831/serendip-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940492/serendip.jpg)[![Serendip - aggregated data](http://4humwhatevery1says.pbworks.com/f/serendip-3-aggregated-data-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104955906/serendip-3-aggregated-data.jpg)[![Serendip - term distibution & metadata views](http://4humwhatevery1says.pbworks.com/f/serendip-4-term-distribution-and-metadata-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104955915/serendip-4-term-distribution-and-metadata.jpg)[![Serendip - topic words in text view](http://4humwhatevery1says.pbworks.com/f/serendip-5-topic-words-in-text-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104955921/serendip-5-topic-words-in-text.jpg)[![Serendip - rank viewer](http://4humwhatevery1says.pbworks.com/f/serendip-6-rank-viewer-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104955927/serendip-6-rank-viewer.jpg)

***

## <a name="termite">Termite</a>

* **Description**:_ [home page](http://vis.stanford.edu/papers/termite)
  * See also: Jason Chuang, Christopher D. Manning, and Jeffrey Heer (2012), ["Termite: Visualization Techniques for Assessing Textual Topic Models"](http://idl.cs.washington.edu/files/2012-Termite-AVI.pdf)
* **Topic modeling workflow**:
  * Termite appears to by a Python system that imports Mallet data files to work on.
* **Notable interpretive features of interface**: Dynamic visual analysis tool designed specifically to augment the user's ability to assess the quality of topic models and topics.
  * The main visual design is a matrix view whose columns (labeled by number on the X axis) are topics, and whose rows are words in those topics (shown on the Y axis). Circles indicating the occurrence of terms in topics (at intersection of X and Y axes) are sized to show the following kinds of metrics:
  * Word frequency _(1st figure at right)_ -- the bigger the circle, the more frequent the word in the topic.
  * Word "saliency" _(compared to frequency in 2nd figure at right)_ -- the bigger the circle, the more salient the word in the topic. ("Saliency" is calculated in a way that answers the question, put roughly, "not only how probable is it that the word occurs in the topic but also how 'distinctive" is the word in its relation the topic. [precise mathematical definition on p. 2 of the Chaung, Manning, & Heer article]).
  * The interface allows users to drill down to other views: "Users can drill down to examine a specifc topic by clicking on a circle or topic label in the matrix. The visualization then reveals two additional views. The word frequency view ... shows the topic's word usage relative to the full corpus. The document view ... shows the representative documents belonging to the topic."
  * The interface allows for various ways to order topics and terms in the visualizations.
  * One of the most important is the ordering of terms in topics through a "seriation algorithm" that incorporates in the metrics collocation frequencies of words with other words _(compared to frequency in 3nd figure at right)_. For example, the right matrix in the 3rd figure at right shows a seriated view of a topic model in which Topic 25 displays a clear clustering of collocated terms (the orange circles).  Such seriated clusters assist in identifying key concepts in topics (not just topic words, which may be hard to understanding in their distribution).
  * Visual analysis tool for assessing topic model quality. Termite uses a tabular layout to promote comparison of terms both within and across latent topics. Uses a novel saliency measure for selecting relevant terms and a seriation algorithm that both reveals clustering structure and promotes the legibility of related terms.
* **Code site**: [GitHub repo](https://github.com/StanfordHCI/termite) (Python scripts; Python version not specified)
  * Starting in 2014, Termite was split into two components (separate repos for each component are linked from the main Termite repo; there do not appear to have been any code updates for two years):
  * Termite Data Server "for processing the output of topic models and providing the content as a web service"
  * Termite Visualization "for visualizing topic model outputs in a web browse"
* **Notes by WE1S team**:
  * _Scott_: I got this working a few years ago and got it mostly working, but for some reason I don't recall it didn't match my research needs at the time.
  * _Alan_: "After spending a week working at implementing Termite, I've concluded that is basically not possible on a Windows system. Termite seems to be basically scripted for Linux or Mac all the way through. On a windows system, I can't compile, can't run scripts, etc.... In regard to Termite: recall that in the past (before 2014), Termite was a simpler system (and also constrained to topic modeling only a single file, rather than folder of files, at a time). Now they have forked their code into a data server (topic modeling creation and local server system), on the one hand, and a visualization system, on the other hand.  It's the data server that has me stuck."
  * _Scott: Update of March 21, 2016_: "I had a look at the Termite code again last night--the old code, rather than the new split system. The one file constraint is actually a file with each document on a separate line. You could write a file from a folder like that (but probably not one with 30,000 documents). That's probably how I did it in the past. It seems possible to inject data at certain points in the pipeline, so you could run Mallet separately and start Termite at the salience calculation stage. But it would take a bit of hacking--sadly something I don't have time to do now. But it's something to keep in mind if we find that the client-side lag time in Serendip is untenable in the future. It may be that neither tool is built for large data sets..."

### Screen Shots

[![Termite - word frequency per topic](http://4humwhatevery1says.pbworks.com/f/termite-1-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104953875/termite-1.jpg)[![Termite - comparison of term frequency vs. saliency rankings for topics](http://4humwhatevery1says.pbworks.com/f/termite-2-term-frequency-vs-saliency-comparison-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104954397/termite-2-term-frequency-vs-saliency-comparison.jpg)[![Termite - comparison of term frequency vs. seriation rankings for topics](http://4humwhatevery1says.pbworks.com/f/termite-2-term-frequency-vs-seriation-comparison-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104954727/termite-2-term-frequency-vs-seriation-comparison.jpg)

***

## <a name="tiara">TIARA</a>

* **Description**:_ [Wei, Furu, et al. "TIARA: A Visual Exploratory Text Analytic System"](http://users.cis.fiu.edu/~lzhen001/activities/KDD_USB_key_2010/docs/p153.pdf) (2010)
* **Topic modeling workflow**:
  * An all-in-one, start-to-finish system; does its own topic modeling. At present, this seems to be a system designed for use in corporate settings to work with corpora of well-structured documents (such as emails and medical information, which are the examples in the article).
* **Notable interpretive features of interface**: A dynamic visualization system that is specialized to Lotus Notes and only usable (apparently) by IBM corporate users.
  * Tiara does its own topic modeling, and in addition derives time-related data (e.g., dates of emails in an email corpus) from the documents.
  * It uses the time-related data to create a timeline of topics in a stratified, layered view in which each topic-layer is populated by key topic words and varies in thickness based on weight in the corpus at the time. Clicking on a topic-layer zoom in on it (widens the layer and shows more topic word detail).
  * Topics can be reordered; the system also supports user merging and splitting of topics.
* **Code site**: [unknown; apparently not open to the public]
* **Notes by WE1S team**:

### Screen Shots

[![Tiara](http://4humwhatevery1says.pbworks.com/f/tiara-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940498/tiara.jpg)

***

## <a name="tom">TOM</a>

* **Description**: Adrien Guille and Edmundo-Pavel Soriano-Morales (2016), ["TOM: A Library for Topic Modeling and Browsing"](http://mediamining.univ-lyon2.fr/people/guille/publications/egc2016_demo.pdf)
* **Topic modeling workflow**:
  * A start-to-finish system. It takes input from a corpus (optionally supplemented by metadata on dates, authors, etc.), then pre-processes it by lemmatizing the text (English or French). It creates two kinds of topic models: LDA and Non-negative Matrix Factorization (NMF). It also uses algorithms based on state-of-the-art computer science research on topic models to help the user optimize the number of topics (see "Parameter Estimation" paragraph on p. 2 of Guille and Soriano-Morales article).
* **Notable interpretive features of interface**: Dynamic visual exploration interface with several views:
  * A _"topic cloud" view_ (figure 1 at right) shows each topic in a bubble that is labeled by the most relevant words and whose diameter indicates its weight in the overall corpus.
  * A _topic view_, a _text view_, (and also _author view_, if there is metadata on authors), as in the lower figures at right.  "For instance, the detailed view about a topic presents the most relevant features, the evolution of the topic frequency through time, the list of related texts and the collaboration network that links authors. The detailed view for a text presents the most significant features, the topic distribution and the most similar texts. Note that some elements may be missing, depending on the meta-data available with the input corpus."
* **Code site**: [Github repo](https://github.com/AdrienGuille/TOM) | [Readme.md](https://github.com/AdrienGuille/TOM/blob/master/README.md) (TOM is a Python 2.7 library.)
* **Notes by WE1S team**:

## Screen Shots

[![TOM](http://4humwhatevery1says.pbworks.com/f/tom-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940504/tom.jpg)

***

## <a name="tome">TOME</a>

* **Description**:
  * NEH Digital Humanities Start-up Grant Proposal (2013): Lauren Klein, Principal Investigator, ["TOME: Interactive TOpic Model and MEtadata Visualization"](http://www.neh.gov/files/grants/georgiatech_interactive_topic_and_metadata_visualization.pdf)
  * NEH Digital Humanities Start-up Grant White Paper (Final Report), [TOMEwhitepaper.pdf](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104296913/TOMEwhitepaper.pdf)
  * See also the related publication: Eisenstein, J., I. Sun and L. Klein. “[Exploratory Text Analysis for Large Document Archives](http://dharchive.org/paper/DH2014/Paper-921.xml).’ _Digital Humanities 2014_.
* **Topic modeling workflow**:
  * Takes input from Mallet.
* **Notable interpretive features of interface**: A dynamic visualization interface that has two views:
  * _"Comparative research in thematic space" view_ (figure at top right) is designed to allow a researcher to compare the topical compositions of multiple different publications with serial issues (such as newspapers). To do so, it focuses at any one time on a selected set of publications in the corpus (e.g., different newspapers) and a selected set of topics of interest (e.g., topics 9-13 in the figure).
  Each publication is represented as a worm-like trail composed of colored circles.
  * Each circle corresponds to an issue of the publication;
  * the color of a circle corresponds to the editor of that run of issues of the publication;
  * the size of a circle represents proportionally how much it is infused by the selected set of topics the user is examining;
  * the position of the circles on the screen (and thus the topography of the worm-like trail for a publication) is determined through a kind of push-pull physics of interaction between the topics being examined. (In detail: _"The topics, here represented as squares, exert a “magnetic” force on each point, pulling each point closer to the topics that are more prominent in that issue. For example, if a given newspaper issue contained words from T9 and T13 in equal measure, with no indication of T10, T11, or T12, then the corresponding circle would be positioned in between the squares representing T9 and T13"_).
  * _Multimodal research in temporal space view_ (figure at bottom right) is designed to allow a researcher to compare the trending of topics in time (and is not focused on specific publications).
  * Typing a word into the search bar at the top of the view brings up in the right panel a list of topics ranked by "relevancy" to the search-word ("relevance—the frequency with which the query appears in each topic").
  * The left panel shows the trends lines of the topics in time, with topics color-coded to match the list of relevant topics. In the trend lines, the thickness of a line indicates the relative weight of a topic at that time in the corpus.
  * Note that "relevance" of a topic to a search-word and weight of the topic in the corpus have no necessary bearing on each other. A topic can be highly relevant to a word (the word is very frequent in the topic), for example, but the topic as a whole can be less frequent in the corpus
* **Code site**: [Github repo](https://github.com/GeorgiaTechDHLab/TOME) (Document file in the repo with instructions is [here](https://github.com/GeorgiaTechDHLab/TOME/blob/master/README.docx?raw=true). The doc begins: "These files are simple HTML files that call the online version of the D3.js library, as well as jQuery. Currently, a version of the D3.js library has been downloaded and saved in the file so the entire project can be pulled up on a local server. I ran this on my machine using the cmd line and python version 2.7 ")
  * Usage and data format notes sent by Lauren Klein to Alan on 1/19/16:
  > "We also generate the topics before formatting them for visualization. We used MALLET at first, but then had to run a custom topic model since our corpus was so large. Once you have the topics, the format is just a five-column CSV, which you can see here:[https://github.com/GeorgiaTechDHLab/TOME/blob/master/a_month_shorter3.csv](https://github.com/GeorgiaTechDHLab/TOME/blob/master/a_month_shorter3.csv)
  > At the moment, the relevance is hand-calculated for one keyword, since we haven’t built the keyword search function yet, but everything else should be fairly self-explanatory.
  > One of the things I’d like to do soon— which may be a good option for you, if you’d like to avoid interacting with MALLET directly— is to hook our interface into an instance of Bookworm, since one of the things that Bookworm does well is offer an API (of sorts) for extracting all sorts of info from a corpus, including topics. It requires a really huge amount of disk space, since it tokenizes (or otherwise indexes) every single word in the corpus beforehand. But in theory, if you can get everything processed— and I’ve also had some issues with the initial install, which I haven’t had time to resolve-- the actual hooking into whatever interface you develop should be relatively easy."
* **Notes by WE1S team**:

## Screen Shots

[![TOME "Trail of Dust" view](http://4humwhatevery1says.pbworks.com/f/tome-1-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940510/tome-1.jpg)[![TOME "Multimodal" and Timeline View](http://4humwhatevery1says.pbworks.com/f/tome-2-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940516/tome-2.jpg)

***

## <a name="topic-browser">The Topic Browser</a>

* **Description**: Gardner, Matthew J, et al., ["The Topic Browser: An Interactive Tool for Browsing Topic Models"](http://cseweb.ucsd.edu/~lvdmaaten/workshops/nips2010/papers/gardner.pdf)
* **Topic modeling workflow**:
  * Topic Browser appears to input data from Mallet.
* **Notable interpretive features of interface**: A dynamic visualization interface:
  * The main navigation and exploring tool is a ranked list of topics labeled by the top two words in each topic _(seen in top figure at right)_. (The interface also allows the user to navigate by documents, words, and "attributes" [metadata].)
  * Because the Topic Browser "incorporates three other pieces of information: attributes (metadata) associated with each document, topic metrics, and document metrics," it can use those metrics to rank and filter the topic list in various ways to enhance interpretation -- e.g., by "simple metrics, such as the number of word tokens and types labeled with the topic, to more complicated metrics such as how dispersed the topic is across documents, or how coherent its words are."
  * "When browsing through topics, the user can filter the topic list by coherence to eliminate from the view those topics that are mostly meaningless and sort by document entropy (a measure of the dispersion of the topic across the documents) to find topics that were used widely throughout the corpus."
  * The interface also can show a concordance-like view of topic words in contest, topic word clouds, top 10 documents associated with each topic, top words in a topic, etc. _(see the other panels in the top figure at right)_.
  * The interface also can plot topics (showing as bars whose length on the Y axis indicates weight) against attributes (metadata) (labeled on the X axis). See for example _the bottom figure at right_, which plots the incidence of three different topics (colored blue, green, red) in documents by a number of different politicians (labeled on the X axis).  Using date metadata would produce a topic timeline.
  * "The second kind of plot that we include is more useful for analyzing and understanding the behavior of the topic model itself. We allow the user to plot two topic metrics against each other and compute a linear regression. This allows the user to see some interesting properties of the topic metrics, such as the fact that document entropy seems to correlate with the logarithm of the number of tokens in the topic, and that coherence does not seem to correlate with any other topic metric. The user can also find outliers, such as topics with low document entropy but a high token count, that can then be examined in the topic page."
* **Code site**: [obsolete code site](http://nlp.cs.byu.edu/topic%20browser) (no new site found)
* **Notes by WE1S team**:
  * _Alan_: The Topic Browser (whose code site can no longer be found) may have be deprecated in favor of the Topical Guide from the same research unit, the [Natural Language Processing Lab](http://wiki.cs.byu.edu/nlp/start) of the Brigham Young University Computer Science Department. See below for [Topical Guide](#topical-guide).

### Screen Shots

[![Topic Browser - overall topic view](http://4humwhatevery1says.pbworks.com/f/topic-browser-1-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940522/topic-browser-1.jpg)[![Topic Browser - plot over attributes view](http://4humwhatevery1says.pbworks.com/f/topic-browser-2-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940528/topic-browser-2.jpg)

***

## <a name="topical-guide">Topical Guide</a>

* **Description**: [Guide (wiki)](https://github.com/BYU-NLP-Lab/topicalguide/wiki) | [Demo](http://tg.byu.edu) (to run the demo, first select the "State of the Union" addresses corpus, then select the "LDA with 100 topics" analysis, then choose among the "topics", "documents", and "visualizations" views)
* **Topic modeling workflow**:
  * A start-to-end system that inputs a corpus of plain-text files (with some metadata added at the top of each file in text form) (see their example text files [here](https://github.com/BYU-NLP-Lab/topicalguide/tree/master/default_datasets/state_of_the_union/documents)). The system then topic models the corpus, opens up a local server, and presents it in a dynamic visualization interface.
* **Notable interpretive features of interface**: A dynamic visualization interface with several views:
  * _Topic view_ (1st figure at right): Shows in column form: topics, topic weights, topic labels, top words in topics (with each column sortable by rank).
  * _Document view_ (2nd figure at right): Shows text of documents (with or without highlighting of topics and topic words); and also shows metadata about each text (including metrics for length, number of tokens, topic entropy)
  * _2D Plots Visualization view_ (3rd figure at right): Plots any two kinds of metadata (e.g., year or author of a document), metrics (e.g., document length, topic entropy), or topic against each other, setting one on the Y axis, the other on the X axis.
  * _"Chord" Diagram Visualization view_ (4th figure at right): arcing chords from one topic positioned on the perimeter of the circle to another topic elsewhere on the circle show correlation (and correlation strength) either by documents (number of docs sharing the topic) or words (number of words the topics share).
  * _"Topics over time" visualization view_ (5th figure at right): Shows proportional weight of topics on the Y axis plotted against year on the X axis (or optionally also other available metadata, such as month, author, title of a work, etc.).
* **Code site**: [Github repo & instructions](https://github.com/BYU-NLP-Lab/topicalguide) (a Python library; Python version not specified)
* **Notes by WE1S team**:
  * _Alan_: to make best use of Topical Guide, we would want to insert some metadata at the top of each of our plain-text document files, which we could do automatically either by scripting information from our scraping spreadsheets or by re-harvesting the text and other data from our spreadsheets.  For example, we could insert at metadata in our files: author, year, month, newspaper title, country, etc.

### Screen Shots

[![Topical Guide - topic view](http://4humwhatevery1says.pbworks.com/f/topical-guide-1-topic-view-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104952996/topical-guide-1-topic-view.jpg) [![Topical Guide - document view](http://4humwhatevery1says.pbworks.com/f/topical-guide-2-document-view-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104953002/topical-guide-2-document-view.jpg)[![Topical Guide - 2D plots  visualization view](http://4humwhatevery1says.pbworks.com/f/topical-guide-3-viz-2d-view-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104953008/topical-guide-3-viz-2d-view.jpg)[![Topical Guide - "chord" diagram visualization view](http://4humwhatevery1says.pbworks.com/f/topical-guide-4-viz-chord-view-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104953014/topical-guide-4-viz-chord-view.jpg)[![Topical Guide - "topics over time" visualization view](http://4humwhatevery1says.pbworks.com/f/topical-guide-5-viz-topics-over-time-view-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104953020/topical-guide-5-viz-topics-over-time-view.jpg)

## <a name="topic-nets">TopicNets</a>

* **Description**: Gretarsson, Brynjar, et al. (research teams from UCSB and UCI) (2012), ["TopicNets: Visual Analysis of Large Text Corpora with Topic Modeling"](http://www.cs.ucsb.edu/~holl/pubs/Gretarsson-2011-ACMTIST.pdf); see also [John O'Donovan's page](http://cs.ucsb.edu/~jod/topicnets.html) (UCSB CS dept.)
  * _Abstract from the article above_: "We present TopicNets, a web-based system for visual and interactive analysis of large sets of documents using statistical topic models. A range of visualization types and control mechanisms to support knowledge discovery are presented. These include corpus and document specific views, iterative topic modeling, search, and visual filtering. Drill-down functionality is provided to allow analysts to visualize individual document sections and their relations within the global topic space. Analysts can search across a data set through a set of expansion techniques on selected document and topic nodes. Furthermore, analysts can select relevant subsets of documents and perform real-time topic modeling on these subsets to interactively visualize topics at various levels of granularity, allowing for a better understanding of the documents."
* **Topic modeling workflow**:
  * TopicNets appears to be a start-to-finish system that does its own topic modeling (or perhaps incorporates Mallet in its processing sequence).
* **Notable interpretive features of interface**: A dynamic visualization interface incorporation a re-iterable real-time topic modeling process to allow for adjustment of the model.
  * The _main visualization metaphor_ is a social network graph whose nodes are topics, documents, and/or entities (e.g., individual or corporate authors, institutions, and other entities sourced from metadata or derived in some other way). Edges and proximity represent the relation between those node types--e.g., between documents and topics. "A novel aspect of the layout includes the use of topic similarity to determine node positions, thus creating visual clusters of topically similar documents."
  * _Real-time rerunning of topic models_: "A key contribution of this work is that TopicNets supports fast, iterative topic modeling which can be run directly from the interactive visualization in near real time to provide better insight into subsets of interest within the larger corpus."
  * In detail: the topic modeling of very large corpora is done in advance or offline; and then iterative real-time topic modeling can be done on smaller subsets of the data.
  * Also, the system can section large documents for topic modeling.
  * _Details on demand_: "When a user selects a node in the graph all the details of that node can be seen in a panel on the right hand side. If the selected node is a document node, a link to view that document is provided. If the selected node is a topic node then links to view all the connected documents are provided. Additional options such as select all neighbor nodes and delete node are also provided on this panel."
  * _Filterable graphs_: "In many cases an analyst is interested in a target subsection of the graph. TopicNets provides multiple methods for filtering the graph in order to get to a visualization of the target information. The user can type in any text and perform a search over the node labels, the top 10 words of all the topics, and/or entire documents. Once the search has completed the user can select a few of the returned nodes from a list, or simply select them all. Once the user has selected a set of nodes of interest he/she can click on a button to visualize only the selected nodes and their immediate neighbors in the graph. Once that button is pressed, all the other nodes are removed from the graph and a new layout is computed.... An alternative filtering method we provide is to manually select one or more nodes in the graph and then make the system remove all nodes not in or connected to the selected nodes."
  * _Graph manipulation by user_: "TopicNets provides a graph interaction mechanism ... which allows an analyst to directly manipulate the visualization by clicking on nodes and moving them around the screen. Single or multiple nodes can be selected through search or a ctrl-click and subsequently moved on the screen by click-and-drag mouse movement.... Using this technique, analysts can mold the graph to highlight interesting features. For example, selecting all documents by a given author and dragging them to one side will deform most graphs into a tree-like layout in which collaborators with the target author are easily identifiable."
* **Code site**: [unknown, but probably findable through colleagues at UCSB]
* **Notes by WE1S team**:

### Screen Shots

[![TopicNets](http://4humwhatevery1says.pbworks.com/f/topic-nets-1-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940537/topic-nets-1.jpg)[![TopicNets - topic similarity view](http://4humwhatevery1says.pbworks.com/f/topic-nets-2-th.jpg)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/104940543/topic-nets-2.jpg)

***

## <a name="twic">TWIC (Topic Words in Context)</a>

* **Description**: From Jonathan Armoza's [Github repository](https://github.com/jarmoza/twic) for TWIC: "Data visualization created by Jonathan Armoza that provides hierarchical, top-down and bottom-up views of LDA topic models generated by the popular topic modeler, MALLET. TWiC was born out of the need for digital humanities researchers to understand how the topic word list outputs from topic modelers like MALLET relate to the texts they attempt to model. In order to do so, the visualization presents users with multiple, related views that portray how topics are distributed throughout the entire collection of texts being modeled, looking from all the way above - the "big data" view - and diving downward to where topic words are situated in their original contexts in the texts themselves. Each successive view as one browses the visualization is then considered part of the larger whole of the previous view, or to put it another way, a subset of texts "underneath" the previous view."
* **Topic modeling workflow**:
  * A .
    * **Notable interpretive features of interface**: (descriptions excerpted fom Jonathan Armoza's [Github repository](https://github.com/jarmoza/twic))
      * _Data Shapes":_
      * _Topic Bullseye:_ "a bullseye-like abstraction of the top N topics of the texts being represented. In the image above, this would represent the top 10 topics of a group of texts. Each ring represents a topic and is given a randomly assigned and unique color. Moving inward from the outside of the shape toward the center, more significant topics are represented, until one arrives at the center, or, the top topic."
      * _Topic Rectangle_: "a shape that utilizes the same paradigm as the topic bullseye, where outer rings (in this case, outer rectangles) represent the top N topics of an individual text. In the image above, this would represent the top 5 topics of one text. At the center of the topic rectangle is a miniature, programmatically-derived (and truncated) view of the text itself and its topic words, each word represented by colored squares among the initial lines of the text. Uncolored words (in a light goldenrod) are words that have been ignored by MALLET."
      * "Graphical Panels" -- "Graphical panels present TWiC's data shapes and their relationships to one another in the model and context of the collection. Informational panels show metadata about those shapes, like the topic word lists themselves and their proportions throughout the various views/levels of the collection. Graphical panels also reveal information about each other as well. With several on the screen, by mousing over data shapes and double-clicking to open underlying views, the user can not only understand the distribution of topics at a particular viewing height in the collection, but also the relation between the topic distribution as seen in those two or more vantages."
      * _Corpus view_ -- "Shows top 10 corpus-level topics of a corpus
      * _Corpus cluster view_ -- "Texts clustered by their top topic and seen as topic bullseyes. Each bullseye is placed at a distance from the corpus's average topic distribution"
      * _Text cluster view_ -- "An example of texts/topic rectangles as viewed underneath a corpus cluster's topic bullseye. Each text is set at a distance from the cluster's average topic distribution"
      * _Individual text view_ -- "A text as selected and viewed from the previous text cluster panel"
      * "Informational Panels"
      * _Topic Bar_ -- "Displays and highlights all topic word lists of the model"
    * **Code site**: [Github repo & instructions](https://github.com/jarmoza/twic)
* **Notes by WE1S team**:

### Screen Shots

[![](http://4humwhatevery1says.pbworks.com/f/twic-1-bullseye-th.png)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/106441998/twic-1-bullseye.png)[![](http://4humwhatevery1says.pbworks.com/f/twic-2-rectangle-th.png)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/106442004/twic-2-rectangle.png) [![](http://4humwhatevery1says.pbworks.com/f/twic-3-corpus-cluster-th.png)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/106442010/twic-3-corpus-cluster.png)[![](http://4humwhatevery1says.pbworks.com/f/twic-4-text-cluster-th.png)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/106442016/twic-4-text-cluster.png)[![](http://4humwhatevery1says.pbworks.com/f/twic-5-individual-text-th.png)](http://4humwhatevery1says.pbworks.com/f/w/file/fetch/106442022/twic-5-individual-text.png)

***

## <a name="other-topic-model-interfaces">Other topic model interfaces hypothesized or mocked up in the research literature (further away from possible implementation by WE1S)<a/>

* Smith, Alison, et al (2014), ["Concurrent Visualization of Relationships between Words and Topics in Topic Models"](https://www.aclweb.org/anthology/W/W14/W14-3112.pdf)
* Veas, Eduardo, and Cecilia di Sciascio (2015), ["Interactive Topic Analysis with Visual Analytics and Recommender Systems"](http://cognitum.ws/wp-content/uploads/2015/06/VeasDiSciascio2015.pdf)

***

## <a name="evaluation-of-topic-models">Evaluation of Topic Models</a>

* Chang, Jonathan, et al. (2009), "[Reading Tea Leaves: How Humans Interpret Topic Models"](http://www.cs.columbia.edu/~blei/papers/ChangBoyd-GraberWangGerrishBlei2009a.pdf)

Option 2: Or upload your HTML document Choose File Indentation level: FORMAT HTML FORMAT HTML IN NEW WINDOW Formatted HTML:
The 4Humanities "WhatEvery1Says" project conducted a comparative analysis in 2016 of the following topic modeling systems/interfaces. As a result, it chose to implement Andrew Goldstone's DFR-browser for its own work.

Last revised November 12, 2016.
