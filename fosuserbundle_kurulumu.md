# FosUserBundle Kurulumu

Fos user bundle, symfony projelerinde sıkça kullanılan ek paketlerden biridir. Üye kaydı, giriş çıkış işlemleri ve güvenlik önlemlerini kapsar.İncelemesini sonraki bölümde yapacağız.

### Adım 1

Composer yardımıyla fos user bundle'ı projemize dahil edelim.

( Ek paketler bölümünde anlatıldı )

### Adım 2

Ek paketimizi proje çekirdeğinde aktifleştirelim

```
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new FOS\UserBundle\FOSUserBundle(),
        // ...
    );
}
```
### Adım 3

Kullanıcı sınıfımızı kendi bundle yapımız altında oluşturalım.

* Doctrine ORM

```
<?php
// src/AppBundle/Entity/User.php

namespace AppBundle\Entity;

use FOS\UserBundle\Model\User as BaseUser;
use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity
 * @ORM\Table(name="fos_user")
 */
class User extends BaseUser
{
    /**
     * @ORM\Id
     * @ORM\Column(type="integer")
     * @ORM\GeneratedValue(strategy="AUTO")
     */
    protected $id;

    public function __construct()
    {
        parent::__construct();
        // your own logic
    }
}
```
* MongoDB 


```
<?php
// src/AppBundle/Document/User.php

namespace AppBundle\Document;

use FOS\UserBundle\Model\User as BaseUser;
use Doctrine\ODM\MongoDB\Mapping\Annotations as MongoDB;

/**
 * @MongoDB\Document
 */
class User extends BaseUser
{
    /**
     * @MongoDB\Id(strategy="auto")
     */
    protected $id;

    public function __construct()
    {
        parent::__construct();
        // your own logic
    }
}```

* CouchDB

```
<?php
// src/AppBundle/CouchDocument/User.php

namespace AppBundle\CouchDocument;

use FOS\UserBundle\Model\User as BaseUser;
use Doctrine\ODM\CouchDB\Mapping\Annotations as CouchDB;

/**
 * @CouchDB\Document
 */
class User extends BaseUser
{
    /**
     * @CouchDB\Id
     */
    protected $id;

    public function __construct()
    {
        parent::__construct();
        // your own logic
    }
}
```
### Adım 4

security.yml dosyamızın içerisindeki herşeyi silip aşağıdaki kodları ekliyoruz.
```
# app/config/security.yml
security:
    encoders:
        FOS\UserBundle\Model\UserInterface: bcrypt

    role_hierarchy:
        ROLE_ADMIN:       ROLE_USER
        ROLE_SUPER_ADMIN: ROLE_ADMIN

    providers:
        fos_userbundle:
            id: fos_user.user_provider.username

    firewalls:
        main:
            pattern: ^/
            form_login:
                provider: fos_userbundle
                csrf_provider: security.csrf.token_manager # Use form.csrf_provider instead for Symfony <2.4

            logout:       true
            anonymous:    true

    access_control:
        - { path: ^/login$, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/register, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/resetting, role: IS_AUTHENTICATED_ANONYMOUSLY }
        - { path: ^/admin/, role: ROLE_ADMIN }
        ```

### Adım 5

config.yml dosyamızın içine aşağıdaki ayar satırlarımızı ekliyoruz.
```
# app/config/config.yml
fos_user:
    db_driver: orm # other valid values are 'mongodb', 'couchdb' and 'propel'
    firewall_name: main
    user_class: AppBundle\Entity\User
    ```
    
Symfony projemizin yönlendirme ayarlarını algılaması için routing.yml dosyamıza aşağıdaki routing ayarlarını ekliyoruz.
```
# app/config/routing.yml
fos_user:
    resource: "@FOSUserBundle/Resources/config/routing/all.xml"```
    
    