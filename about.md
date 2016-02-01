---
layout: page
title: About
comments: true
permalink: /about/
---

My name is Jun Sun. This is my personal site, and it follows the philosophy of minimalism. I mainly put my little stuffs here, like:

* reviews/understanding/comments of academic papers/tech reports
* codes/programs/git repos
* random thoughts
* other interesting/boring stuffs

It is basically a place to help myself organize things, but discussions are all welcomed.


{% if post.comments %}
<div id="disqus_thread"></div>
<script>
(function() {  // DON'T EDIT BELOW THIS LINE
 var d = document, s = d.createElement('script');
 s.src = '//yfiua-github-io.disqus.com/embed.js';
 s.setAttribute('data-timestamp', +new Date());
 (d.head || d.body).appendChild(s);
 })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endif %}
