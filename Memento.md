###### tags: `Design Patterns`
# Memento



## Definition:
在不破壞封裝性的前提下，捕獲一個物件的內部狀態，並在該物件之外保存這個狀態．這樣以後就可將該物件恢復到原先保存的狀態．

## 應用情境




## 範例:
```php=
abstract class Component{
        protected $name;

        public function Component($name){
                $this->name = $name;
        }

        public abstract function Add($c);
        public abstract function Remove($c);
        public abstract function Display($depth);

}

class Leaf extends Component{
        public function Leaf($name){
                parent::Component($name);
        }

        public function Add($c){
                echo "Can not add to a leaf";
        }
        public function Remove($c){
                echo "Cannot remove from a leaf";
        }
        public function Display($depth){
                echo "depth=".$depth." name=".$this->name."\n";
        }

}

class Composite extends Component{
        private $children = Array();

        public function Composite($name){
                parent::Component($name);
        }

        public function Add($c){
                $this->children[] = $c;
        }

        public function Remove($c){
                for($i=0;$i<count($this->children);$i++){
                        if($this->children[$i]===$c){
                                array_splice($this->children, $i, 1);
                        }
                }
        }
        public function Display($depth){
                echo "composite depth=".$depth." name=".$this->name."\n";
                foreach($this->children as $item){
                        $item->Display($depth+2);
                }

        }
}

$root = new Composite("root");
$root->Add(new Leaf("Leaf A"));
$root->Add(new Leaf("Leaf B"));
$root->Add(new Leaf("Leaf C"));
$leaf = new Leaf("Leaf D");
$root->Add($leaf);
$root->Display(2);

$root->Remove($leaf);
$root->Display(2);

```
#### 參考頁面:


