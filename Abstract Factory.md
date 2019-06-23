###### tags: `Design Patterns`
# Abstract Factory


## Definition:
提供一個建立一系列相關或相互依賴物件的介面，而無需指定他們具體的類別．

## 應用情境


## 範例:
```php=

interface IDepartment{
        public function Insert($department);
        public function GetDepartment($id);

}

class SqlserverDepartment implements IDepartment{
        public function Insert($department){
                echo "Insert a department data=".$department->getName()." in SQL Server\n";
        }

        public function GetDepartment($id){
                echo "In the SQL Server, get a record of Department by using id=".$id."\n";
        }

}

class AccessDepartment implements IDepartment{
        public function Insert($department){
                echo "Insert an department data=".$department->getName()." in Access\n";
        }

        public function GetDepartment($id){
                echo "In the Access Server, get a record of Department by using id=".$id."\n";
        }

}


interface IFactory{
        public function CreateUser();
        public function CreateDepartment();
}

class SqlServerFactory implements IFactory{
        public function CreateUser(){
                return new SqlserverUser();
        }
        public function CreateDepartment(){
                return new SqlserverDepartment();
        }
}

class AccessFactory implements IFactory{
        public function CreateUser(){
                return new AccessUser();
        }
        public function CreateDepartment(){
                return new AccessDepartment();
        }

}

interface IUser{
        public function Insert($user);
        public function GetUser($id);
}

class SqlserverUser implements IUser{
        public function Insert($user){
                echo "Insert an User=".$user->getName()." in the SQL Server\n";
        }
        public function GetUser($id){
                echo "Get an User data from SQL server by using id=".$id."\n";
        }
}

class AccessUser implements IUser{
        public function Insert($user){
                echo "Insert an User=".$user->getName()." in the Access\n";
        }
        public function GetUser($id){
                echo "Get an User data from Access by using id=".$id."\n";
        }
}

class User{
        private $_id;
        public function getID(){
                return $this->$_id;
        }
        public function setID($value){
                $this->_id = $value;
        }
        private $name;
        public function getName(){
                return $this->name;
        }
        public function setName($value){
                $this->name = $value;
        }
}

class Department{
        private $_id;
        public function getID(){
                return $this->$_id;
        }
        public function setID($value){
                $this->_id = $value;
        }
        private $name;
        public function getName(){
                return $this->name;
        }
        public function setName($value){
                $this->name = $value;
        }
}

$user = new User();
$user->setName("Wisely");
$user->setID(1);

$department = new Department();
$department->setName("Develpement");
$department->setID(4);

$factory = new SqlServerFactory();
$iu = $factory->CreateUser();

$iu->Insert($user);
$iu->GetUser(1);

$id = $factory->CreateDepartment();
$id->Insert($department);
$id->GetDepartment(1);


```
#### 參考頁面: