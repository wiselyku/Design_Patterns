###### tags: `Design Patterns`
# Strategy


## Definition:
Strategy Pattern 定義了演算法家族，分別封裝起來，讓它們之間可以互相替換，此模式讓演算的變化不會影響到使用演算法的客戶。

## 應用情境:



## 範例:
以下為PHP程式範例
```php=
abstract class CashSuper {

    public abstract function acceptCash($money);
}

class CashNormal extends CashSuper {

    public function acceptCash($money) {
        return $money;
    }

}

class CashRebate extends CashSuper {

    private $moneyRebate = 1;

    public function CashRebate($rebate) {
        $this->moneyRebate = $rebate;
    }

    public function acceptCash($money) {
        return $money * $this->moneyRebate;
    }

}

class CashContext {

    private $cs;

    public function CashContext(CashSuper $csuper) {
        $this->cs = $csuper;
    }

    public function GetResult($money) {
        return $this->cs->acceptCash($money);
    }

}

$cash = new CashContext(new CashNormal());
echo $cash->GetResult(500);
echo "<BR>";
$cashTow = new CashContext(new CashRebate(0.3));
echo $cashTow->GetResult(500);

```
#### 參考頁面:

