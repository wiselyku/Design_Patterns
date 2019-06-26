###### tags: `Design Patterns`
# Iterator

## Definition:
迭代器模式，提供一種方法依序存取一個聚合物件中各個元素，而又不暴露該物件的內部表示．


## 應用情境


## 範例:
```php=
abstract class Iterators{
        public abstract function First();
        public abstract function Next();
        public abstract function IsDone();
        public abstract function CurrentItem();
}

abstract class Aggregate{
        public abstract function CreateIterator();
}

class ConcreteIterator extends Iterators{
        private $aggregate;
        private $current = 0;

        public function ConcreteIterator($aggregate){
                $this->aggregate = $aggregate;
        }

        public function First(){
                return $this->aggregate->GetItem(0);
        }

        public function Next(){
                $ret = null;
                $this->current++;
                if($this->current < $this->aggregate->GetCount()){
                        $ret = $this->aggregate->GetItem($this->current);
                }
                return $ret;
        }

        public function IsDone(){
        //      echo $this->current."\n";
        //      echo $this->aggregate->GetCount()."\n";
                return $this->current >= $this->aggregate->GetCount() ? true : false;
        }

        public function CurrentItem(){
                return $this->aggregate->GetItem($this->current);
        }
}

class ConcreteAggregate extends Aggregate{
        private $items = Array();
        public function CreateIterator(){
                return new ConcreteIterator($this);
        }
        public function GetCount(){
                return count($this->items);
        }
        public function AddItem($value){
                $this->items[] = $value;
        }
        public function GetItem($index){
                if($this->items[$index]==null){
                        echo "error: there is nothing in index=".$index."\n";
                }else{
                        return $this->items[$index];
                }
        }
}

$a = new ConcreteAggregate();
$a->AddItem("hello");
$a->AddItem("world");

$i = new ConcreteIterator($a);
$first = $i->First();
while(!$i->IsDone()){
        echo $i->CurrentItem()."\n";
        $i->Next();
}



```
#### 參考頁面: