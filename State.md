###### tags: `Design Patterns`
# State

## Definition:
當一個物件的內在狀態改變時允許改變其行為，這個物件看起來像是改變了其類別．

## 應用情境
狀態模式主要解決的是當控制一個物件狀態轉換的條件運算式過於複雜時的情況．把狀態的判斷邏輯轉移到表示不同狀態的一系列類別當中，可以把複雜的判斷邏輯簡化．

## 範例:
```php=
abstract class State{
        public abstract function WriteProgram($work);
}

class ForenoonState extends State{

        public function WriteProgram($work){
                if($work->GetHour()<12){
                        echo "it is before 12 o'clock\n";
                }
                else{
                        $work->SetState(new NoonState());
                }
        }
}

class NoonState extends State{
        public function WriteProgram($work){
                if($work->GetHour()<13){
                        echo "it is around 13 o'clock\n";
                }else{
                        $work->SetState(new AfternoonState());
                }
        }
}

class AfternoonState extends State{
        public function WriteProgram($work){
                if($work->GetHour()<17){
                        echo "it is around 14-17 o'clock\n";
                }else{
                        $work->SetState(new EveningState());
                }
        }
}

class EveningState extends State{
        public function WriteProgram($work){
                if($work->GetHour()<21){
                        echo "it is around 18-21 o'clock\n";
                }else{
                        $work->SetState(new SleepingState());
                }
        }
}

class SleepingState extends State{
        public function WriteProgram($work){
                echo "it is sleeping time";
        }
}


class RestState extends State{
        public function WriteProgram($work){
                echo " the current time is ".$work->GetHour();
        }
}

class Work{
        private $current;
        public function Work(){
                $this->current = new ForenoonState();
        }

        private $hour;
        public function GetHour(){
                return $this->hour;
        }
        public function SetHour($value){
                $this->hour = $value;
        }
        private $finish=false;
        public function GetTaskFinish(){
                return $this->finish;
        }
        public function SetTaskFinish($value){
                $this->finish->$value;
        }

        public function SetState($s){
                $this->current = $s;
        }

        public function WriteProgram(){
                $this->current->WriteProgram($this);
        }

}

$emergencyProjects = new Work();
$emergencyProjects->SetHour(9);
$emergencyProjects->WriteProgram();
$emergencyProjects->SetHour(12);
$emergencyProjects->WriteProgram();
$emergencyProjects->WriteProgram();
$emergencyProjects->SetHour(13);
$emergencyProjects->WriteProgram();
$emergencyProjects->WriteProgram();

```
#### 參考頁面: