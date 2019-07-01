###### tags: `Design Patterns`
# Single responsibility principle

## Definition:
在物件導向編程領域中，單一功能原則（Single responsibility principle）規定每個類都應該有一個單一的功能，並且該功能應該由這個類完全封裝起來。所有它的（這個類的）服務都應該嚴密的和該功能平行（功能平行，意味著沒有依賴）。
## 應用情境:


## 範例:
```php=
/* 下面範例，一個class只做一種圖形的面積算法 */

abstract class Shape{
        private $length;
        abstract function AreaSum();
}

class Circle extends Shape{
        private $length;

        public function __construct($length){
                $this->length = $length;
        }
        public function AreaSum(){
                return 3.14*$this->length*$this->length;
        }
}

class Square extends Shape{
        private $length;

        public function __construct($length){
                $this->length = $length;
        }
        public function AreaSum(){
                return $this->length*$this->length;
        }
}

class AreaCalculator{
        protected $shapes;

        public function __construct($shapes = Array()){
                $this->shapes = $shapes;
        }

        public function Sum(){
                $sum = 0;
                foreach($this->shapes as $shape){
                        $sum = $sum + $shape->AreaSum();
                }
                return $sum;
        }

        public function Output(){
                return $this->Sum();
        }
}


$shapes = array(new Circle(2), new Square(10));

$areas = new AreaCalculator($shapes);
echo $areas->Output()."\n";

```

#### 參考頁面
1. https://zh.wikipedia.org/wiki/%E5%8D%95%E4%B8%80%E5%8A%9F%E8%83%BD%E5%8E%9F%E5%88%99

