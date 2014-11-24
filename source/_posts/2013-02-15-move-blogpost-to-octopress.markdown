---
layout: post
title: "Move blogpost to octopress"
date: 2013-02-15 14:42
comments: true
categories: 
- linux 
- blog
---
If you are in Taiwan like me, need to go to /etc/hosts and add one line
```
173.194.72.132 <blogname>.blogspot.tw 
``` 

Pack your blogspot post (the max-results in gist is 500, adjust it for you need)
```
$ git clone git://gist.github.com/4958888
$ cd 4958888
$ sh ./bloggerImport.sh <blogname> 
```

After that, you will get a _posts directory, but before copy it to source, we need something to convert html to markdown

I use reverse_markdown :

[https://github.com/xijo/reverse_markdown](https://github.com/xijo/reverse_markdown)

or in ruby envirament simply do :
```
gem install reverse_markdown
```

When is's all ready, we use some command to convert all posts to markdown :
```
$ cd _posts
$ find -name "*.html" | sed -e 's/\.html//' | xargs -n 1 -I @ sh -c 'reverse_markdown @.html > @.markdown'
$ rm *.html # remove all html files
```

And finally, we can deploy :
```
$ cd ..
$ cp _posts <to_your_octopress_source>/source
$ cd <to_your_octopress_source>
$ rake generate && rake deploy
```