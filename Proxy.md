###### tags: `Design Patterns`
# Proxy


## Definition:
Proxy Pattern 為其他物件提供一種代理以控制對這個物件的存取。


## 應用情境:
瀏覽器開啟網頁時，利用代理去抓圖片。



## 範例:
```php=
abstract class Subject {

    public abstract function Request($str);
}

class RealSubject extends Subject {

    public function Request($str) {
        echo "Request is " . $str . "<BR>";
    }

}

class Proxy extends Subject {

    private $real_subject;

    function __construct() {
        $this->real_subject = new RealSubject();
    }

    public function Request($str) {
        $this->real_subject->Request($str);
    }

}

$request = new Proxy();
$request->Request("I need a pen. ");
```
#### 參考頁面:
