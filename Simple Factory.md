
###### tags: `Design Patterns`
# Simple Factory


## Definition:




## 應用情境:
如果要寫一個計算機的程式，用物件導向的方式去實作，希望可以隨時新增新的Operation (例如: 加法，減法，除法，乘法，開根號...等等)，如果都寫在同一個class就會違反 Open-Closed Principle，那用Simple Factory Pattern 來實作。



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

class OperationAdd extends Operation{
    
    public function getResult(){
        $result = 0;
        $number1 = $this->getNumber1();
        $number2 = $this->getNumber2();
        $result = $number1 + $number2;
        return $result;
    }
}

class OperationSub extends Operation{
    
    public function getResult() {
        $result = 0;
        $number1 = $this->getNumber1();
        $number2 = $this->getNumber2();
        $result = $number1 - $number2;
        return $result;        
    }
    
}


class OperationFactory{
    
    public static function createOperate( $operate){
        switch($operate){
            case "+":
                $oper = new OperationAdd();
                break;
            case "-":
                $oper = new OperationSub();
                break;
        }
        return $oper;
    }
    
}

$add_result = OperationFactory::createOperate("+");
$add_result->setNumber1(2);
$add_result->setNumber2(3);
echo $add_result->getResult();
```

#### 參考頁面:
