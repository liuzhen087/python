pythonh中re模块  
Python使用re模块提供了正则表达式处理的能力  
常量  
|常量|说明|  
|--|--|  
|re.M re.MULTILINE|多行模式|  
|re.S re.DOTALL|单行模式|  
|re.I re.IGNORECASE|忽略大小写|  
|re.X re.VERBOSE|忽略表达式中的空白字符|  
使用|位或运算开启多种选项  

方法  
编译  
re.compile(pattem,flags=0)  
设定flags,编译模式,返回正则表达式对象regex.  
pattem就是正则表达式字符串,flags是选项.正则表达式需要被编译,为了提高效率,这些编译后的结果被保存,下次使用同样的pattern的时候,就不需要再次编译  

re的其他方法为了提高效率都调用了编译方法,就是为了提速  

单次匹配  
re.match(pattern,string,flags=0)  
regex.match(string[,pos[,endos]])  
match匹配从字符串的开头匹配,regex对象match方法可以重设开始位置和结束位置.返回match对象  
```
import re

t = """bootle\nabc\nbig\nbac"""

r = re.match('a',t)
print(r)
``` 

re.search(pattern,string,flags=0)  
regex.search(string[,pos[,endpos]])  
从头搜索直到第一个匹配,regex对象serch方法可以重新设定开始位置和结束位置,返回match对象  
```
import re

t = """bootle\nabc\nbig\nbac"""

r = re.search('a',t)
print(r)
regax = re.compile('b',re.M)
r = regax.search(t)
print(r)
```

re.fullmatch(pattern,string,flags=0)  
regex.fullmatch(string[,pos[,endos]])  
整个字符串和正则表达式匹配  



全文搜索  
re.findall(pattern,string,flags=0)  
regex.findall(string[,pos[,endpos]])  
对整个字符串,从左至右匹配,返回匹配项的列表  

re.finditer(pattern,string,flags=0)  
regex.finditer(string[,pos[endpos]])  
对整个字符串,从左到右匹配,返回所有匹配项,返回迭代器  
注意每次迭代返回的是match对象  


匹配替换  
re.sub(pattern,replacement,string,count=0,flags=0)  
regex.sub(replacement,string,count=0)  
使用pattern对字符串string进行匹配,对匹配项使用repl替换  
replacement可以是string bytes function  

re.subn(pattern, replacement,string,count=0,flags=0)  
regex.subn(replacement,string,count=0)  
同sub返回一个元组(new_string,number_of_subs_made)  

```
import re

t = """bootle\nabc\nbig\nbac"""

regax = re.compile('b')
r = regax.sub('hello',t)
print(r)
r = regax.sub('hello',t,1) #替换1次
print(r)
```
分割字符串  
字符串的分割函数split,太难用  
re.split(pattern,string,maxsplit=0,flags=0)  
re.split分割字符串  
```
import re 
s = """
(hello.word!)
"""
print(re.split('[\.()\s,]+',s))
```

分组  
使用小括号的pattern捕获的数据被放到了组group中.  
match search函数可以返回match对象;findall返回字符串列表,finditer返回一个个match对象  
如果pattern中使用了分组,如果有匹配的结果,会在match对象中  
1. 使用了group(N)方式对应分组,1到N是对应的分组,0返回整个匹配的字符串,N不写缺省为0  
2. 如果使用了命名分组,可以使用group('name')的方式取分组
3. 也可以使用groups()返回所有组  
4. 使用groupdict()返回所有命名的分组  
```
import re 
t = """bootle\nabc\nbig\nbac"""

regex = re.compile('b\w+'\n(?P<name>\w+)\n(?P<name>\w+))
r = regex.match(t)
print('match',r)
print(r.group(1),r.group(2))
print(r.group(0).encode())
print(r.groupdict())
```





