###### tags: `Design Patterns`
# Builder

## Definition:
Builder Pattern 將一個複雜物件的構件與它的表示分離，使得同樣的構建過程可以建立不同的表示。


## 應用情境


## 範例:
```php=
abstract class PersonBuilder {

    public abstract function BuildHead();

    public abstract function BuildBody();

    public abstract function BuildArmLeft();

    public abstract function BuildArmRight();

    public abstract function BuildLegLeft();

    public abstract function BuildLegRight();
}

class PersonThinBuilder extends PersonBuilder {

    public function BuildHead() {
        echo "Build a head <BR>";
    }

    public function BuildBody() {
        echo "Build a body <BR>";
    }

    public function BuildArmLeft() {
        echo "Build a left arm <BR>";
    }

    public function BuildArmRight() {
        echo "Build a right arm <BR>";
    }

    public function BuildLegLeft() {
        echo "Build a left leg <BR>";
    }

    public function BuildLegRight() {
        echo "Build a right leg <BR>";
    }

}

class PersonDirector {

    private $pb;

    public function __construct(PersonBuilder $person) {
        $this->pb = $person;
    }

    public function CreatePerson() {
        $this->pb->BuildHead();
        $this->pb->BuildBody();
        $this->pb->BuildArmLeft();
        $this->pb->BuildArmRight();
        $this->pb->BuildLegLeft();
        $this->pb->BuildLegRight();
    }

}

$builder = new PersonThinBuilder();
$person = new PersonDirector($builder);
$person->CreatePerson();
```
#### 參考頁面: