###### tags: `Design Patterns`

# Flyweight


## Definition:
享元模式，運用共用技術有效地支援大量細粒度的物件．


## 應用情境



## 範例:
```php=

abstract class WebSite{
        abstract function UseWebSite();
}

class ConcreteWebSite extends WebSite{
        private $name="";

        public function ConcreteWebSite($name){
                $this->name = $name;
        }

        public function UseWebSite(){
                echo "網站分類: ".$this->name." \n";
        }

}

class WebSiteFactory{
        private $flyweights = Array();

        public function GetWebSiteCategory($key){
                if(empty($this->flyweights[$key])){
                        $this->flyweights[$key] = new ConcreteWebSite($key);
                }
                return $this->flyweights[$key];
        }

        public function GetWebSiteCount(){
                return count($this->flyweights);
        }
}

$f = new WebSiteFactory();
$fx = $f->GetWebSiteCategory("產品展示");
$fx->UseWebSite();

$fy = $f->GetWebSiteCategory("產品展示");
$fy->UseWebSite();

$fz = $f->GetWebSiteCategory("部落格");
$fz->UseWebSite();

$fn = $f->GetWebSiteCategory("部落格");

echo "目前網站分類總數= ".$f->GetWebSiteCount()."\n";

```
#### 參考頁面: