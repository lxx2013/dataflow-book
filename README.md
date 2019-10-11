# 源代码转 latex algo 带换行
>复制到浏览器控制台中执行下面代码,再执行`example{\n string; \n }`.b()
```js
String.prototype.b = function (space_num = 2) {
    var space = (x) => Array(x).fill(' ').join('')
    var stage = 0, result = ''
    var str = this.replace(/({|})/g, '\\$1') // 在 { } 左侧添加\\
    var stmts = str.split('\n').map(x => x.trim()).filter(x=>!!x)
	console.log(stmts)
    stmts.forEach((s,idx)=>{
        if (/\}/.test(s)) stage--
        result += (stage?`  \\hspace*{${stage} pc} `:'') + s + ((idx>=stmts.length-1)?'': '\\\\\n')
        if (/\{$/.test(s)) stage++
    })
    return `\n\\begin{algorithm}\\label{algo:costream}\n`+result+
`\n\\end{algorithm}\n`
}
```
