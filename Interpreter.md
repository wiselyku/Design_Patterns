###### tags: `Design Patterns`
# Interpreter

## Definition:
解譯器模式，給定一個語言，定義它的文法的一種表示，並定義一個解譯器，這個解譯器使用該表示來解釋語言中的句子．

## 應用情境


## 範例:
```php=

abstract class AbstractExpression{
        abstract function Interpret($context);
}

class TerminalExpression extends AbstractExpression{
        public function Interpret($context){
                echo "終端解譯器\n";
        }
}

class NonterminalExpression extends AbstractExpression{
        public function Interpret($context){
                echo "非終端解譯器\n";
        }

}

class Context{
        private $input;
        public function getInput(){
                return $this->input;
        }
        public function setInput($value){
                $this->input = $value;
        }

        private $output;
        public function getOutput(){
                return $this->output;
        }
        public function setOutput($value){
                $this->output = $value;
        }
}

$context = new Context();
$list = Array();
$list[] = new TerminalExpression();
$list[] = new NonterminalExpression();
$list[] = new TerminalExpression();
$list[] = new NonterminalExpression();

foreach($list as $item){
        $item->Interpret($context);
}

```
#### 參考頁面: