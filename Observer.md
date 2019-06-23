###### tags: `Design Patterns`
# Observer

## Definition:



## 應用情境


## 範例:
```php=
interface Subject{
        public function Attach($observer);
        public function Detach($observer);
        public function Notify();
//      private $SubjectState;
        public function getSubjectState();
        public function setSubjectState($value);

}

class Boss implements Subject{

        private $observers = Array();
        private $action;
        private $SubjectState;
        public function Attach($observer){
                $this->observers[] = $observer;
        }

        public function Detach($observer){
                for($i=0;$i<count($this->observers);$i++){
                        if($this->observers[$i]===$observer){
                                array_splice($this->observers, $i, 1);
                        }
                }
        }

        public function Notify(){
                foreach($this->observers as $observer){
                        $observer->Update();
                }
        }

        public function getSubjectState(){
                return $this->SubjectState;
        }

        public function setSubjectState($value){
                $this->SubjectState = $value;
        }

}

abstract class Observer{
        protected $name;
        protected $subject;

        public function Observer($name, $sub){
                $this->name = $name;
                $this->subject = $sub;
        }

        public abstract function Update();

}

class StockObserver extends Observer{
        public function StockObserver($name, $sub){
                $this->name = $name;
                $this->subject = $sub;
        }

        public function Update(){
                echo "我是".$this->name." ，我老闆回來了，我要趕快認真工作！";
        }

}

$wisely = new Boss();
$stark = new StockObserver("Tony Stark", $wisely);
$wisely->Attach($stark);

$wisely->setSubjectState("我回來了");
$wisely->Notify();


```
#### 參考頁面: