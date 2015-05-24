# Kavramlar

Symfony Türkçe Kitabında kullanacağım kavramlar temel olarak şunlardır.

**Twig;** Twig bir php tema motorudur.Html sayfaları içerisine php kodu yazılmadan php çalıştırılmasına yarar.Örnek kullanımı şu şekildedir.
```
index.html.twig
```
**Routing;** Routing ( Yönlendirme ) Symfony projemizdeki Url kontrolünü sağlayacağımız .yml uzantılı dosyalardır.Örnek kullanımı şu şekildedir;
```
routing.yml
```
**Controller;** Projemizin php kodlarını yazacağımız kısmıdır.Routing üzerinden gelen veriyi alıp işleyip tekrar routing üzerinden twig'e basmaya yarar,fonksiyonlarımızı içerir.Örnek kullanımı şu şekildedir.
```
DefaultController.php
```
***
Temel kavramlar bunlar olup projemizin MVC yapısını temsil etmektedir.