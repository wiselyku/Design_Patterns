###### tags: `Design Patterns`
# Decorator

## Definition:
Decorator Pattern 動態地給一個物件加入一些額外的職責，就增加功能來說，Decorator Pattern 比產生子類別更為靈活。

## 應用情境


## 範例一
以下為PHP程式範例
```php=
abstract class Component {

    public abstract function Operation();
}

class ConcreteComponent extends Component {

    public function Operation() {
        echo "具體物件的操作<BR>";
    }

}

abstract class Decorator extends Component {

    protected $component;

    public function SetComponent(Component $comp) {
        $this->component = $comp;
    }

    public function Operation() {
        if ($this->component != NULL) {
            $this->component->Operation();
        }
    }

}

class ConcreteDecoratorA extends Decorator {

    private $addedState;

    public function Operation() {
        parent::Operation();
        $this->addedState = "New State";
        echo "具體裝飾物件A的操作<BR>";
    }

}

class ConcreteDecoratorB extends Decorator {

    public function Operation() {
        parent::Operation();
        $this->AddedBehavior();
        echo "具體裝飾物件B的操作<BR>";
    }

    public function AddedBehavior() {
        echo "具體裝飾物件B新增的操作<BR>";
    }

}

$obj = new ConcreteComponent();
$dec1 = new ConcreteDecoratorA();
$dec2 = new ConcreteDecoratorB();

$dec1->SetComponent($obj);
$dec2->SetComponent($dec1);
$dec2->Operation();
```
#### 參考頁面:
