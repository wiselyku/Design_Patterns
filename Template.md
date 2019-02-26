###### tags: `Design Patterns`
# Template

## Definition:
Template Pattern 定義一個操作中的演算法的骨架，而將依些步驟延遲到子類別中。Template Pattern使得子類別可以不改變一個演算法的結構即可重定義該演算法的某些特定步驟。


## 應用情境


## 範例:
```php=
abstract class AbstractClass {

    public abstract function PrimitiveOperation1();

    public abstract function PrimitiveOperation2();

    public function TemplateMethod() {
        $this->PrimitiveOperation1();
        $this->PrimitiveOperation2();
        writeln("");
    }

}

class ConcreteClassA extends AbstractClass {

    public function PrimitiveOperation1() {
        writeln("具體類別A方法1實現");
    }

    public function PrimitiveOperation2() {
        writeln("具體類別A方法2實現");
    }

}

class ConcreteClassB extends AbstractClass {

    public function PrimitiveOperation1() {
        writeln("具體類別B方法1實現");
    }

    public function PrimitiveOperation2() {
        writeln("具體類別B方法2實現");
    }

}

$template = new ConcreteClassA();
$template->TemplateMethod();

$template = new ConcreteClassB();
$template->TemplateMethod();

function writeln($line_in) {
    echo $line_in . "<br/>";
}
```



#### 參考頁面: