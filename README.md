# artbergmann
Migrating existing Joomla! site for Canadian musician, Art Bergmann, to Jekyll rendered static site.

### Helper commands

**Bulk rename filenames in directory**
```
qmv -A --format=destination-only
```
http://www.nongnu.org/renameutils/

**Add numbers to start of each line of text**
```
%!nl -nrz -w2 -s'-'
```

**Remove Joomla! importer front matter from lyrics pages**
```
sed -i '4,8d' */*/lyrics/*.markdown
```

**Change lyric pages' layouts to "page"**
```
sed -i 's/layout: post/layout: page/g' */*/lyrics/*.markdown
```

**Remove all remaining front matter and style title for lyrics**
```
sed -i '1,2d;s/title: /##/;4d' */*/lyrics/*.markdown
```

**Include lyrics in album page**
```
ls -c lyrics/*.markdown | sort | awk '{print "{% include_relative " $0 " %}"}' >> index.markdown
```
## Reformatting pages / posts using vim

**Break monolithic one line articles on &lt;br /&gt; tag**
```
:%s/<br \/>/^M/g
```
Note: The ^M is generated by CTRL-V + RETURN

**Strip HTML tags**
```
:%s/<[^>]*>//g
```

**Trailing two spaces for markdown &lt;br /&gt;**
```
:%s/$/  /g
```

**Remove non-breaking spaces that occupy a line**
```
%s/^&nbsp;$//g
```

**Remove smart double-quotes**
```
:%s/&rdquo;\|&ldquo;/\"/g
```

**Remove smart single-quotes**
```
:%s/&rsquo;\|&ldsqo;/\'/g
```

###Tips
1. These will be stored in vim's history, so cycle through them using the up/down arrow after entering command mode.
2. ~~Record a macro on the first page by pressing 'q' followed by any letter (name of macro); then press 'q' when finished recording; and use the macro by pressing '@' followed by the letter.~~
