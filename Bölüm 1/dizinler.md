# Dizinler
Konuya giriş yapmadan önce symfony'i bir insan olarak hayal edelim.

Bu insanın elinde bir oyuncak bebek olsun.Bu bebek bizim projemizdeki bundle yani kod bohçası.

Projemizi bundle adı verilen yapı altında geliştireceğiz.

Dizinleri insana benzeterek daha akılda kalıcı bir anlatım yapacağım.

İlk olarak **app** dizini;
Dizin insanın yani symfony'nin beynidir.İçerisindekiler şöyledir;
* 
app
 * 
cache ( Cache'ler )
 * 
config ( Ayarların yapıldığı yer  )
 * 
logs ( Log kayıtlarının tutulduğu yer  )
 * 
Resources ( Kaynaklar )
    

Dizinleri yer alır.

Config dizini altında 
```
config.yml
parameters.yml
routing.yml
security.yml
```
Temel ayar dosyaları barınmaktadır.Bunları insanın beyni olarak düşünebilirsiniz.Bu yaml dosyalarıda beynimizdeki karar mekanizmalarının ayarlarıdır.

Cache ve loglar projemizin geliştirme,test ve yayın sürecinde alacağı hata mesajlarını depolar ve zamanla şişer,bunlar hafıza olarak düşünülebilir.

Resources dizini temel olarak base.html.twig dosyasını barındırır.Bu projemizdeki taslak html css dosyaları için koyulmuştur.İnsanın iskeletine benzetebiliriz.



