###### tags: `Design Patterns`
# Bridge

## Definition:
橋接模式，將抽象部分與他的實現部分分離，使他們都可以獨立地變化


## 應用情境


## 範例:
```php=
abstract class Implement{
        public abstract function Operation();
}

class ConcreteImplementorA extends Implement{
        public function Operation(){
                echo "具體實現Ａ的方法執行\n";
        }
}

class ConcreteImplementorB extends Implement{
        public function Operation(){
                echo "具體實現Ｂ的方法執行";
        }
}

class Abstraction{
        protected $implementor;

        public function SetImplementor($implementor){
                $this->implementor = $implementor;
        }

        public function Operation(){
                $this->implementor->Operation();
        }

}

class RefinedAbstraction extends Abstraction{
        public function Operation(){
                $this->implementor->Operation();
        }
}

$ab = new RefinedAbstraction();
$ab->SetImplementor(new ConcreteImplementorA());
$ab->Operation();


```
#### 參考頁面: