
# CODE EXAMPLES
## Download file via Web Console
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

## Create Class in Web Console
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

## Control Window Sidebar
- Open WebDev Tool
- `window.scrollby(x, y);`
