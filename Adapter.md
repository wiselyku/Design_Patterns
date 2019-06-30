###### tags: `Design Patterns`
# Adapter

## Definition:
轉接器模式，將一個類別的介面轉換成客戶希望的另外一個介面．轉接器模式使得原本由於介面不相容而不能一起工作的那些類別可以一起工作．

## 應用情境



## 範例:
```php=
abstract class Player{
        protected $name;
        public function Player($name){
                $this->name = $name;
        }
        abstract function Attack();
        abstract function Defense();
}

class Forwards extends Player{
        public function Forwards($name){
                $this->name = $name;
        }
        public function Attack(){
                echo "Forward ".$this->name." go attacing\n";
        }
        public function Defense(){
                echo "Forward ".$this->name." back to defense\n";
        }
}

class Center extends Player{
        public function Center($name){
                $this->name = $name;
        }
        public function Attack(){
                echo "Center ".$this->name." go attacing\n";
        }
        public function Defense(){
                echo "Center ".$this->name." back to defense\n";
        }
}

class Guards extends Player{
        public function Guards($name){
                $this->name = $name;
        }
        public function Attack(){
                echo "Guard ".$this->name." go attacing\n";
        }
        public function Defense(){
                echo "Guard ".$this->name." back to defense\n";
        }
}

class ForeignCenter{
        private $name;
        public function GetName(){
                return $this->name;
        }
        public function SetName($name){
                $this->name = $name;
        }

        public function Attack(){
                echo "Foreign Center ".$this->name." attack the basket\n";
        }
        public function Defense(){
                echo "Foreign Center".$this->name." defense the basket\n";
        }
}

class Translator extends Player{
        private $wjzf;
        public function Translator($name){
                $this->wjzf = new ForeignCenter();
                $this->name = $name;
                $this->wjzf->SetName($name);
        }
        public function Attack(){
                $this->wjzf->Attack();
        }
        public function Defense(){
                $this->wjzf->Defense();
        }
}

$b = new Forwards("Bob");
$b->Attack();

$m = new Guards("Michael");
$m->Attack();

$ym = new Translator("Yao");
$ym->Attack();
$ym->Defense();

```
#### 參考頁面: