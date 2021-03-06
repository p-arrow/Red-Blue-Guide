## TABLE OF CONTENTS
1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/PHP.md#basics)
2. [CODE EXAMPLES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/PHP.md#code-examples)

<br />

## BASICS
- **Dangerous Commands that perform execution (previous Input Validation is important!)**
   - `exec`
   - `passthru`
   - `proc_open`
   - `shell_exec`
   - `system`
- **var_dump**:
   - `var_dump(json_obj/array)`: Show info about object/array
   - `echo var_dump(variable)."<br>"`
- **echo**:
   - `echo "\n";`: newline 
   - `echo $array[index];`: show value of index 
- **print_r**:
   - `print_r()`: Show info about variable 
- **include()**:
   - `include()`: include php script into another one
   - `<?php include 'footer.php';?>`: if footer.php is not available, **script execution will continue**
- **require()**:
   - `require()` / `require_once`: include php script into another one
   - `<?php require 'footer.php';?>`: if footer.php is not available, **script execution will stop**
   - require_once is not performed, if required php script is already available
- **String concatenation**: 
   - `$string = "x";`
   - `$s = 42 . $string;`: $s becomes "42x"
- **Interactive shell**:
   - `$ php -a` 
- **preg_match**:
   - `preg_match(pattern, input, matches, flags, offset)`
   - If "matches" is given, it contains all results
   - `$matches[0]` contains text that matches complete pattern
   - `$matches[1]` contains text that matches first partial pattern
- **Comparisons**:
   - Loose comparison using ==/!=      --> Both variables have "the same value"
     - Security Impact Explained: [php type juggling](http://turbochaos.blogspot.com.au/2013/08/exploiting-exotic-bugs-php-type-juggling.html)
     - Example: `"uuid": "../../../etc/passwd"; "sig": 0;`: comparing string (uuid), which gets hashed, and integer (sig) could lead to boolean True
     - If the computed hash starts with `0` (followed by a letter) or starts by a letter: `a to f`; it will be equal to `0`
     - So, you can basically bypass the signature check due to buggy "PHP Loose Comparison"
   - Strict comparison using ===/!==   --> Both variables have "the same type and the same value"
 
```
php > var_dump("1" === 1);
bool(false)
php > var_dump("1" == 1);
bool(true)
php > var_dump("a" == 0);
bool(true)
php > var_dump("1' or 1=1" == 1);
bool(true)
php > var_dump("<script>alert(1)</script>" == 0);
bool(true)
```
<br />

## CODE EXAMPLES
### preg_patterns
```
<?php
# /i = ignore case

$str = "Visit W3Schools";
$pattern = "/w3schools/i"; 
echo preg_match($pattern, $str);

# Output: 1 (True)
?>
```

```
<?php
# \b = word boundary (to find whole words) 

echo preg_match("/\bweb\b/i", "PHP is the first choice for web development.");
# Output: 1 (True)
?>
```

```
<?php
# Task: Get hostname from URL
# (?...) = Non-capturing group
# (?...)? = between 0 or 1 of preceding token
# [^/]+ = Match any char except "/", 1 or more

preg_match('@^(?:http://)?([^/]+)@i', "http://www.php.net/index.html", $hit);
$host = $hit[1];
echo $host;
# Output: www.php.net

# Get last two segments of hostname 
preg_match('/[^.]+\.[^.]+$/', $host, $hit);
echo "Domain Name is: {$hit[0]}\n";
# Output: php.net
?>
```

### Loop through Array
```
<?php
$numbers = array("1", "2", "3", "4");
foreach ($numbers as $item){
	echo $item . "\n";
}
?>
```

### XOR-Algorithm via For Loop
```
<?php
function xor_encrypt($in) {
    $key = 'secret';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
    return $outText;
}
?>
```
