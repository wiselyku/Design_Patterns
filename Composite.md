###### tags: `Design Patterns`
# Composite

## Definition:
組合模式，將物件組合成樹形結構以表示「部分-整體」的層次結構．組合模式使得用戶對單個物件和組合物件的使用具有一致性．


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