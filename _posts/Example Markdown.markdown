---
layout: post
title:  "Title!"
date:   2017-04-06 22:33:33 +0000
categories: jekyll update
comments: true
---

HEADINGS

# This is an H1

## This is an H2

###### This is an H6

INLINE QUOTES

> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.


UNORDERED LISTS

*   Red
*   Green
*   Blue


ORDERED LISTS

Ordered lists use numbers followed by periods:

1.  Bird
2.  McHale
3.  Parish

But could equally be"

1.  Bird
1.  McHale
1.  Parish


LINKS

[Link text](URL here "Optional Title"){:target="_blank"} <--_ This will open in a new tab

IMAGES

![image alt text]({{site.url}}/assets/image-title.jpg "optional title")



CODE BLOCKS

To produce a code block in Markdown, simply indent every line of the block by at least 4 spaces or 1 tab.


To indicate a span of code inside a paragraph, wrap it with backtick quotes (`).       `

CODE SNIPPETS

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}






HORIZONTAL RULES

Three or more hyphens, asterisks, or underscores on a line by themselves. If you wish, you may use spaces between the hyphens or asterisks. Each of the following lines will produce a horizontal rule:

* * *

***

- - -

--------



EMPHASIS

*single asterisks*

_single underscores_

**double asterisks**

__double underscores__



BACKSLASH ESCAPES
Markdown provides backslash escapes for the following characters:

\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark









Include all of the below to get comments!


{% if page.comments %} <div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://futuremorlock.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript> {% endif %}
