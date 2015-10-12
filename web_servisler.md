##Web Servisler

Projemizin **platform bağımsız** çalışabilmesi için belli formatlarda verileri vermemiz gerekecektir, **xml** ve **json** gibi,bunu symfony uygulama çatısında nasıl çıkaracağımızı görelim.

---
### Adım 1

Controller içerisinde use komutunu kullanacağız.

```
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
```

### Adım 2

Controller'da ilgili işlemlerimizi yaptıktan sonra, göndereceğimiz yanıtı hazırlayalım.

```
$yanit = array();
```

Return komutunda şu değişiklikleri yapıyoruz.
```
$response = new Response(json_encode($yanit));
            $response->headers->set('Content-type', 'application/json; charset=utf-8');
            $response->setStatusCode(200);
            return $response;
        
```

Birleştirecek olursak;
```
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
..
public indexAction(Request $request)
{
 
    $yanit = array();
 
    $response = new Response(json_encode($yanit));
    $response->headers->set('Content-type', 'application/json; charset=utf-8');
    $response->setStatusCode(200);
    return $response;
}```

İlk web servisimizi yazmış olduk.