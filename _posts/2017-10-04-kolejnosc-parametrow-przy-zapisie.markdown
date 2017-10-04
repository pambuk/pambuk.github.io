---
layout: post
title:  "Kolejność parametrów przy zapisie modelu z mutatorem"
date:   2017-10-04 21:50:54 +0200
categories: php laravel
---

Model `Operation` zapisuje wartość (`value`) na podstawie typu operacji (`type`), 
więc wartość może być z minusem lub nie.
Przy dodawaniu operacji z formularza wszystko działało normalnie, ale test się już wysypywał.

Rozwiązaniem okazała się zmiana kolejności parametrów i nie ma tu znaczenia czy operacja dodawana jest
przez statyczny `create()` czy poprzez przypisanie każdego parametru do już istniejącego obiektu.

Ten kod działa:

<!-- You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works. -->

<!-- Jekyll also offers powerful support for code snippets: -->

{% highlight php %}
$operation = $operationService->create([
    'type' => OperationTypes::INCOME,
    'value' => 30,
]);
{% endhighlight %}

ale ten już nie:

{% highlight php %}
$operation = $operationService->create([
    'value' => 30,
    'type' => OperationTypes::INCOME,
]);
{% endhighlight %}

Niby logiczne ale dla mnie nowość.

<!-- Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/ -->
