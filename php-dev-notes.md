# Tips in writing PHP code

This file describe the tricks that can be used in writing the PHP codes

# 1. `"text"` and `'text'`
PHP does have different intepretions on the string that is surrounded by `''` (single quote) and `""` (double quotes). When used in normal string it does results in the result.
```php
<?php
$a="text"; //text
$b='text'; //test
?>
```
The only difference between those is when the string is surrounded using `''`(single quote) the string will be interpreted "as it is". This means nearly all espace sequences are not interpreted except the `\'` that used to escape the `'` in the string. Also, the variable are not expanded in single quoted.
```php
<?php
$hurray='Hurray';
echo '\n'; //outputs "\n"
echo '$hurray ! My bonus is here'; //outputs "$hurray ! My bonus is here"
echo 'it\'s'; //outputs "it's"
?>
```
Conversely if the string is surrounded using `"` (double quotes) the espace sequences will be interpreted and the variables will be expanded
```php
<?php
$name='花';
$dict=array(
'name'=>'花',
'ruby'=>'はな',
'color'=>'赤い'
);
echo "あら、きれいな{$name}がさいている"; //outputs "あら、きれいな花がさいている"
/*
*output:
*<pre>名称：花
*色：赤い
*</pre>
*/
echo "<pre>名称：{$dict['name']}\n色：{$dict['color']}</pre>"; 
?>
```
# 2. Anything outside `<?php ?>` are echos
TBC
