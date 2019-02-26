###### tags: `Design Patterns`
# Factory

## Definition:
Factory Pattern 定義一個用於建立物件的介面，讓子類別決定實體化哪一個類別。Factory Pattern 使一個類別的實例化延遲到其子類別。


## 應用情境


## 範例:
以下範例用PHP實作
```php=
abstract class Operation {

    private $number1;
    private $number2;

    public function setNumber1($num1) {
        $this->number1 = $num1;
    }

    public function setNumber2($num2) {
        $this->number2 = $num2;
    }

    public function getNumber1() {
        return $this->number1;
    }

    public function getNumber2() {
        return $this->number2;
    }

    public abstract function getResult();
}

class OperationAdd extends Operation {

    public function getResult() {
        $result = 0;
        $number1 = $this->getNumber1();
        $number2 = $this->getNumber2();
        $result = $number1 + $number2;
        return $result;
    }

}

class OperationSub extends Operation {

    public function getResult() {
        $result = 0;
        $number1 = $this->getNumber1();
        $number2 = $this->getNumber2();
        $result = $number1 - $number2;
        return $result;
    }

}

interface IFactory {

    public function CreateOperation();
}

class AddFactory implements IFactory {

    public function CreateOperation() {
        return new OperationAdd();
    }

}

class SubFactory implements IFactory {

    public function CreateOperation() {
        return new OperationSub();
    }

}

$operFactory = new AddFactory();
$oper = $operFactory->CreateOperation();
$oper->setNumber1(12);
$oper->setNumber2(13);
echo $oper->getResult();
```
#### 參考頁面:
