###### tags: `Design Patterns`
# Mediator

## Definition:
仲介者模式，用一個仲介物件來封裝一系列的物件互動．仲介者使各物件不需要顯式地互相參考，從而使其耦合鬆散，而且可以獨立地改變他們之間的互動．


## 應用情境


## 範例:
```php=
abstract class Mediator{
        abstract function Send($message, $colleague);
}

abstract class Colleague{
        protected $mediator;

        public function Colleague($mediator){
                $this->mediator = $mediator;
        }

}

class ConcreteMediator extends Mediator{
        private $colleague1;
        private $colleague2;

        public function SetColleague1($value){
                $this->colleague1 = $value;
        }

        public function SetColleague2($value){
                $this->colleague2 = $value;
        }

        public function Send($message, $colleague){
                if($colleague==$this->colleague1){
                        $this->colleague1->Notify($message);
                }else{
                        $this->colleague2->Notify($message);
                }
        }
}

class ConcreteColleague1 extends Colleague{
        public function ConcreteColleague1($mediator){
                $this->mediator = $mediator;
        }

        public function Send($message){
                $this->mediator->Send($message, $this);
        }

        public function Notify($message){
                echo "Colleague1 received a message: ".$message."\n";
        }
}

class ConcreteColleague2 extends Colleague{
        public function ConcreteColleague2($mediator){
                $this->mediator = $mediator;
        }

        public function Send($message){
                $this->mediator->Send($message, $this);
        }

        public function Notify($message){
                echo "Colleague2 received a message: ".$message."\n";
        }
}

$m = new ConcreteMediator();

$c1 = new ConcreteColleague1($m);
$c2 = new ConcreteColleague2($m);

$m->SetColleague1($c1);
$m->SetColleague2($c2);

$c1->Send("Do you have lunch already?\n");
$c2->Send("Not yet! Do you want to give us a treat?\n");


```
#### 參考頁面: