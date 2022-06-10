# virtualbox
```
sudo apt update

sudo apt upgrade
```
```
sugo apt install apache2 mysql-server php libapache2-mod-php php-mysql
```
```
sudo apt install net-tools
```
```
ifconfig
```
```
cd /var/www/html

ls
```
```
sudo apt install vim
```
```
sudo vim info.php
```
```
<?php
  phpinfo();
?>

:wq! 強制存檔離開
```
```
sudo apt install phpmyadmin
```
```
sudo mysql -u root mysql

UPDATE user SET plugin='mysql_native_password' WHERE User='root';
FLUSH PRIVILIGES;
exit
```
```
sudo mysql_secure_installation
y 2 y y y
```
## 到瀏覽器去輸入ip位置/phpmyadmin
輸入帳號密碼

如果登入phpmyadmin失敗
```
sudo mysql -p -u root

CREATE USER '(自己想要的帳號)'@'%' IDENTIFIED BY '(密碼)';
GRANT ALL PRIVILEGES ON *.* TO '(帳號)'@'%';
exit
```
進入畫面設定資料
建立完資料庫之後回去終端機的指令
```
sudo nano (資料庫名稱).php
```
```
<?php
          $host ='localhost';
          $dbuser ='(主機的帳號)';
          $dbpw ='(自己的密碼)';
          $dbname =$_GET['a'];
          $link = mysqli_connect($host,$dbuser,$dbpw,$dbname);
          if(empty($link)){
             print mysqli_error($link);
             die("資料庫連接失敗");
             exit;  }
          if(!mysqli_select_db($link,$dbname)){
              die("資料選取失敗");  }
          else {
               echo "連接".$dbname."資料庫成功<br>";  }
          mysqli_query($link,"SET NAMES'UFT-8'");
           $sql  ="SELECT* FROM (下一層資料庫名稱)";
           $result = mysqli_query($link,$sql);
           if($result) {
              $num =mysqli_num_rows($result);
              echo $_GET['a'];
              echo "資料表有".$num."筆資料<br>";  }
           $result =mysqli_query($link,$sql);
           while($row =mysqli_fetch_array($result,MYSQLI_ASSOC)) {
                printf("第%s筆資料: %s<br>, %s<br>, %s<br>",$row["number"],$row["id"],$row["name"],$row["gender"]);
}
?>
```



```
<html>
<head><title>php連接資料庫MysQl</title></head>
<body>
輸入要搜尋的資料庫
<form action='(資料庫名稱).php'>
<input type='text' name='a' />
<button type='submit'>送出<button>
</form>
</body>
</html>
```



```
<?php
          $host ='localhost';
          $dbuser ='(主機的帳號)';
          $dbpw ='(自己的密碼)';
          $dbname ='(資料庫名稱)';
          $link = mysqli_connect($host,$dbuser,$dbpw,$dbname);
          if($link){
             mysqli_query($link, 'SET NAMES uff8');
             echo("正確連接資料庫");
          }
          else{
             echo "不正確連接資料庫</br>" . mysqli_connect_error();
          }
          
          //sql語法存在變數中
          $sql ="INSERT INTO '(資料庫名稱)' ('number','id','name','gender') VALUE ('1' ,'b1042001','姓名','男')";
          
          //用mysqli_query方法執行(sql語法)將變數存在變數中
          $result =mysqli_query($link,$sql);
          
          //如果有異動到資料庫數量(更新資料庫)
          if(mysqli_affected_rows($link)>0){
          //如果有一筆以上代表有更新
          //mysqli_insert_id可以抓到第一筆的id
          $new_id =mysqli_insert_id($link);
            echo "新增後的id為{$new_id}";
          }
          elseif(mysqli_affected_rows($link)==0){
            echo"無資料新增";
          }
          else{
            echo "{$sql}語法執行失敗，錯誤訊息:" . mysqli_error($link);
          }
          mysqli_close($link);
?>
```
