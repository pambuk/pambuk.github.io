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