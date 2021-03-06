#Putting the old OED online

The Oxford English Dictionary is the most detailed dictionary of English, and an incredible resource.

The first edition is out of copyright. This means we can legally adapt it forthe web.

The hard work is already done: scans of almost all volumes exist on the Internet Archive.  But they're hidden away, and inaccessible.

So let's build a better interface to them.

Further reading:

- http://en.wikipedia.org/wiki/Oxford_English_Dictionary
- http://ohuiginn.net/mt/2009/02/the_oxford_english_dictionary.html [links to- scans of most volumes of the dictionary.
- http://ohuiginn.net/oed -- VERY rough interface to the scans [requires a djvu browser plugin]
- http://lists.canonical.org/pipermail/kragen-tol/2005-October/000794.html -- proposal from Kragen Sitaker, who did much of the initial work to get the scans online

#Refresh Oxford

The good thing about this project, is there's plenty we can achieve in a day., Here are my rough plans in stages, from what we could certainly achieve in one day, to more advanced ideas which we definitely won't

STAGE ONE: usable interface to the scanned pages.
A website where you can choose volume and page of the OED, and be shown the scan of that page. Some navigation to flip back and forward through pages. There are 2 options for this:

A) Using djvu. This format lets you call up an individual page of a book without downloading more than that. We have (most volumes of) the oed in djvu format, and I've put up a basic interface at http://ohuiginn.net/oed

The problem is that you need a browser plugin to view djvu files. This doesn't seem very helpful for the casual user.

B) Using png. Do on-the-fly conversion of pages from djvu to png, as they are requested.

C) both (a) and (b). djvu interface, with png as a fallback

STAGE TWO: finding (approximately) the correct page for a word

You enter a word, and the service flips to approximately the right page of the dictionary. Again we have 2 alternatives: one easy, the other easy harder but better:

A) just guess based on the letters covered in each volume, and the position of the word searched for in an alphabetical list of english words. So if 'refresh' is, say, 30% of the way through the English words starting R, we look for it on page 300 of the 1000-page R volume

B) Half-hearted OCR. We can't easily do full OCR on the dictionary -- the text is in columns, and includes a lot of characters in odd alphabets. But we can do basic OCR, giving us an (inaccurate, incomplete) list of the characters on each page. Then we find the most common prefix of those words. i.e. if a page contains 50 words starting JER-, that probably means we are on the JER- page of the dictionary.

STAGE THREE: more advanced things involving OCR. Not likely to happen in a single day.

---

Further ideas:

 - facebook integration: share a word. [select text and extract]?
 - link to a word -- link to a particular place in the page
 - skimlinks-style linking -- read through a page, insert links to [some] words in the OED
 - 'Dead Word of the Day'. extract interesting words (as images) from a particular page). blog them

# Image server

To return images as png:
$ cd node
$ node oed.js

images will be available through /page/png?vol=6a&page=180

currently running on oed.ohuiginn.net:
http://oed.ohuiginn.net/page/png?vol=6a&page=180


#PDFMINER

The most (only?) reliable way of extracting headwords from a pdf page of the oed seems to be using pdfminer
A command-line version like the following seems to work:
 python pdf2txt.py -p 250 -t html /var/www/oed/oed04arch.pdf 

This requires the latest version of pdfminer from https://github.com/euske/pdfminer/blob/master/docs/programming.html
There's a current bug in the pdfminer setup -- you _need_ to build the CJK language bit ("make cmap"), or it won't work at all


#CREDITS

*  Dan O'Huiginn [http://ohuiginn.net]
*  Chuck Dixon [https://github.com/chvckd]
*  Warren Hobden

