# Tips in writing PHP code

This file describe the tricks that can be used in writing the PHP codes

# 1. `"text"` and `'text'`
PHP does have different intepretions on the string that is surrounded by `''` (single quote) and `""` (double quotes). When used in normal string it does results in the result.
```php
<?php
$a="text"; //text
$b='text'; //text
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
# 2. `<?=...?>`
In PHP the `<?=...?>` is  shorthands for `<?php echo ...;?>`
So the following code snippets are equivalent
```php
<?php
echo "hello";
?>
```
```php
<?="hello"?>
```
# 3. Anything outside `<?php ?>` are ignored and outputed
Technically PHP ignores anything outside the `<?php ?>` and outputs it directly to the output.
## Example 1: Basics
If the original php code are as below:
```php
<html>
<head></head>
<body>
<?php
echo time();
?>
</body>
</body>
```
The PHP parser will ignore anything outside the `<>php ?>` and output it directly to the output. Making the above code techinically equivalent with the following
```php
<?php
echo "<html>\n<head></head>\n<body>";
echo time();
echo "</body></body>";
?>
```
## Example 2: Usage inside code blocks (function blocks and if-else if-else blocks etc)
By using the same property we can simplify this:
```php
<?php
if(intval($_GET['value'])<20){
echo "<div id=\"result\">The value you have provided is less than 20</div>";
}
else{
echo "<div id=\"result\">The value you have provided is more or equal than 20</div>";
}
?>
```
into
```php
<?php
if(intval($_GET['value'])<20){
?>
<div id="result">The value you have provided is less than 20</div>;
<?php
}
else{
?>
<div id="result">The value you have provided is more or equal than 20</div>;
<?php
}
?>
```
## Example 3: Mixture with shorthand (`<?=...?>`)
Similar with the Example 2 but with the `$_GET['value']` outputted too
```php
<?php
if(intval($_GET['value'])<20){
?>
<div id="result">The value you have provided is less than 20 (<?=$_GET['value']?>)</div>;
<?php
}
else{
?>
<div id="result">The value you have provided is more or equal than 20 (<?=$_GET['value']?>)</div>;
<?php
}
?>
```
[Reference](https://www.php.net/manual/en/language.basic-syntax.phpmode.php)
