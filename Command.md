###### tags: `Design Patterns`
# Command

## Definition:
命令模式，將一個請求封裝為一個物件，讓你可用不同的請求對客戶進行參數化;對請求排隊或記錄請求日誌，以及支援可取消的操作．

## 應用情境


## 範例:
```php=

abstract class Command{
        protected $receiver;
        public function Command($receiver){
                $this->receiver = $receiver;
        }

        abstract function ExecuteCommand();
}

class BakeMuttonCommand extends Command{
        public function BakeMuttonCommand($receiver){
                $this->receiver = $receiver;
        }
        public function ExecuteCommand(){
                $this->receiver->BakeMutton();
        }
        public function toString(){
                return "BakeMutton";
        }
}
class BakeChickenWingCommand extends Command{
        public function BakeChickenWingCommand($receiver){
                $this->receiver = $receiver;
        }
        public function ExecuteCommand(){
                $this->receiver->BakeChickenWing();
        }
        public function toString(){
                return "BakeChickenWing";
        }
}

class Barbecuer{
        public function BakeMutton(){
                echo "烤羊肉串\n";
        }

        public function BakeChickenWing(){
                echo "烤雞翅\n";
        }
}

class Waiter{
        private $orders = Array();
        private $muttonCount = 2;
        private $chickenWingCount = 2;
        public function SetOrder($command){
                if($command->toString()=="BakeMutton" && $this->muttonCount<=0 ){
                        echo "服務生:羊肉串沒有囉，請點別的燒烤\n";
                }else if($command->toString()=="BakeChickenWing" && $this->chickenWingCount<=0){
                        echo "服務生:雞翅串沒有囉，請點別的燒烤\n";
                }else{
                        $this->orders[] = $command;
                        echo "增加訂單: ".$command->toString()."\n";
                        if($command->toString()=="BakeMutton"){
                                $this->muttonCount--;
                        }else{
                                $this->chickenWingCount--;
                        }
                }
        }
        public function CancelOrder($command){
                for($i=0;$i<count($this->orders);$i++){
                        if($this->orders[$i]==$command){
                                array_splice($this->orders, $i, 1);
                                if($command->toString()=="BakeMutton"){
                                        $this->muttonCount++;
                                }else{
                                        $this->chickenWingCount++;
                                }
                                echo "取消訂單: ".$command->toString()."\n";
                        }
                }
        }
        public function Notify(){
                foreach($this->orders as $command){
                        $command->ExecuteCommand();
                }
        }
}

$boy = new Barbecuer();
$bakeMuttonCommand1 = new BakeMuttonCommand($boy);
$bakeMuttonCommand2 = new BakeMuttonCommand($boy);
$bakeChickenWingCommand1 = new BakeChickenWingCommand($boy);
$bakeMuttonCommand3 = new BakeMuttonCommand($boy);
$girl = new Waiter();


$girl->SetOrder($bakeMuttonCommand1);
$girl->Notify();
$girl->SetOrder($bakeMuttonCommand2);
$girl->Notify();
$girl->SetOrder($bakeChickenWingCommand1);
$girl->Notify();
$girl->SetOrder($bakeMuttonCommand3);
$girl->Notify();

```
#### 參考頁面: