##E-Posta İşlemleri

Symfony uygulama çatısında e-posta göndermek için **swiftmailler** adlı ek paketi kullanacağız. Bu ek paket symfony kurulumunu yaptığımızda içerisinde kurulu olarak geliyor.

E-posta göndereceğimiz proje içerisinde ilgili ayarları yapalım.E-posta gönderebileceğimiz ücretsiz servisleri yazının sonunda paylaşacağım.

---

### Adım 1


İlk olarak, **config.yml** dosyamıza aşağıdaki satırları değişiklik yapmadan ekliyoruz.

```
# app/config/config.yml
swiftmailer:
    transport: "%mailer_transport%"
    host:      "%mailer_host%"
    username:  "%mailer_user%"
    password:  "%mailer_password%"
```
    
**config.yml** içerisinde aşağıdaki seçeneklerde kullanılabilir.

```
transport (smtp, mail, sendmail, veya gmail)
username
password
host
port
encryption (tls, veya ssl)
auth_mode (plain, login, veya cram-md5)
spool
type (Mesajları nasıl kuyruğa alacağınız veya ek dosyaların boyutu ne kadar olacak ayarları için gereklidir)
path (Postaların depo edileceği dizin)
delivery_address (Postaların gönderici adresi kısmında görünecek kısmı)
disable_delivery (Geliştirme aşamasında e-posta gönderimini devre dışı bırakmak için)
```

### Adım 2

Parameters.yml içerisindeki ilgili ayarlamaları yapalım.
```
#app\config\parameters.yml

parameters:
    database_driver: pdo_mysql
    database_host: localhost
    database_port: null
    database_name: db
    database_user: db
    database_password: pass
    mailer_transport: smtp
    mailer_host: "HOST"
    mailer_user: "USER"
    mailer_password: "PASS"
    mailer_port: 465
    secret: TOKEN
    ```
    
### Adım 3

Son adım olarak nasıl controller içerisinde e-postamızı gönderdiğimizi görelim.

```
public function indexAction($name)
{
    $message = \Swift_Message::newInstance()
        ->setSubject('Hello Email')
        ->setFrom('send@example.com')
        ->setTo('recipient@example.com')
        ->setBody(
            $this->renderView(
                // app/Resources/views/Emails/registration.html.twig
                'Emails/registration.html.twig',
                array('name' => $name)
            ),
            'text/html'
        )
        /*
         * If you also want to include a plaintext version of the message
        ->addPart(
            $this->renderView(
                'Emails/registration.txt.twig',
                array('name' => $name)
            ),
            'text/plain'
        )
        */
    ;
    $this->get('mailer')->send($message);

    return $this->render(...);
}
```

---

Ücretsiz olarak e-posta gönderebileceğiniz servislerden bazıları; Gmail, Mandrill, Amazon SES,SendGrid servislerini örnek verebiliriz.