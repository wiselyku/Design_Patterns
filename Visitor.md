###### tags: `Design Patterns`
# Visitor

## Definition:
訪問者模式，表示一個作用於某物件結構中的各元素之操作，它使你可以在不改變各元素之類別的前提下，定義作用於這些元素的新操作．

## 應用情境


## 範例:
```php=
abstract class Action{
        abstract function GetManConclusion($concreteElementA);
        abstract function GetWomanConclusion($concreteElementB);
}

abstract class Person{
        abstract function Accept($visitor);
}

class Success extends Action{
        public function GetManConclusion($concreteElementA){
                echo "男人成功時，背後多半有一個偉大的女人\n";
        }

        public function GetWomanConclusion($concreteElementB){
                echo "女人成功時，背後大多有一個不成功的男人\n";
        }
}

class Failing extends Action{
        public function GetManConclusion($concreteElementA){
                echo "男人失敗時，悶頭喝酒，誰也不用勸\n";
        }
        public function GetWomanConclusion($concreteElementB){
                echo "女人失敗時，眼淚汪汪，誰也勸不了\n";
        }
}

class Amativeness extends Action{
        public function GetManConclusion($concreteElementA){
                echo "男人戀愛時，凡事不懂也要裝懂\n";
        }

        public function GetWomanConclusion($concreteElementB){
                echo "女人戀愛時，遇事懂也裝作不懂\n";
        }
}

class Man extends Person{
        public function Accept($visitor){
                $visitor->GetManConclusion($this);
        }
}

class Woman extends Person{
        public function Accept($visitor){
                $visitor->GetWomanConclusion($this);
        }
}

class ObjectStructure{
        private $elements = Array();
        public function Attach($element){
                $this->elements[] = $element;
        }
        public function Detach($element){
                for($i=0;$i<count($this->elements);$i++){
                        if($this->elements[$i]==$element){
                                array_splice($this->elements, $i, 1);
                        }
                }
        }
        public function Display($visitor){
                foreach($this->elements as $person){
                        $person->Accept($visitor);
                }
        }
}

$o = new ObjectStructure();
$o->Attach(new Man());
$o->Attach(new Woman());

$v1 = new Success();
$o->Display($v1);

$v2 = new Failing();
$o->Display($v2);

$v3 = new Amativeness();
$o->Display($v3);

```
#### 參考頁面: