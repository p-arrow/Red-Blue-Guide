
# CODE EXAMPLES
1. [DOWNLOAD FILE](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Javascript.md#download-file-webconsole)
2. [CREATE CLASS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Javascript.md#create-class-webconsole)
3. [CONTROL WINDOW SIDEBAR](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Javascript.md#control-window-sidebar-webconsole)
4. [CSRF](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Javascript.md#csrf)
5. [NORMALIZE STRING](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Coding/Javascript.md#normalize-string)

<br />

## Download File (WebConsole)
```
function downloadURI(uri, name) 
{
    var link = document.createElement("a");
    // If you don't know the name or want to use
    // the webserver default set name = ''
    link.setAttribute('download', name);
    link.href = uri;
    document.body.appendChild(link);
    link.click();
    link.remove();
}
downloadURI("https://example.com/file.png", "captcha1")
```
<br />

## Create Class (WebConsole)
```
class Animals {
  constructor(name, age) {
    this.name = name;
    this.specie = age;
  }
  
  sing(){
    return `${this.name} can sing.`;
  }
  
  dance(){
    return `${this.name} can dance.`;
  }
}  

let bingo = new Animals("bingo", "10");
console.log(bingo);
console.log(bingo.sing());
```
<br />

## Control Window Sidebar (WebConsole)
- Open WebDev Tool
- `window.scrollby(x, y);`

<br />

## CSRF
```
<a href="http://www.harmless.com/" onclick="
  var f = document.createElement('form');
  f.style.display = 'none';
  this.parentNode.appendChild(f);
  f.method = 'POST';
  f.action = 'http://www.example.com/account/destroy';
  f.submit();
  return false;">To the harmless survey</a>
```

<br />

## Normalize String
- Details: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize)
```
x = "ã" 

console.log('Unicode codepoint:', 
  x.charCodeAt(0).toString(16),
  x.charCodeAt(1).toString(16))
// → Unicode codepoint: 61 303

console.log('Normalize:', x.normalize('NFC'))
console.log('Normalize:', x.normalize('NFD'))
console.log('Normalize:', x.normalize('NFKC'))
console.log('Normalize:', x.normalize('NFKD'))
```

## MEASURE PERFORMANCE
- Could be used for **Sidechannel Attacks**
```
<script>
  const t0 = performance.now();
  for (let i = 0; i < 10; i++) {
    console.log(i);
  }
  const t1 = performance.now();
  console.log(`Call to doSomething took ${t1 - t0} milliseconds.`);
</script>
```
