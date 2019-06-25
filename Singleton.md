###### tags: `Design Patterns`
# Singleton

## Definition:
獨體模式保證一個類別僅有一個實體，並提供一個存取他的全域訪問點．


## 應用情境


## 範例:
```php=
class Singleton{
        private static $instance;

        private function Singleton(){
                echo "we new a object\n";
        }

        public static function GetInstance(){
                if(self::$instance==null){
                        self::$instance = new Singleton();
                }
                echo "get the object\n";
                return self::$instance;
        }
}

$s1 = Singleton::GetInstance();
$s2 = Singleton::GetInstance();

if($s1==$s2){
        echo "we are the same object\n";
}

```
#### 參考頁面: