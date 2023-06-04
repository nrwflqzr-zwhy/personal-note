# Idea方法注释模板

## 创建模板

![image-20220822105246690](E:\Note\Java\Idea方法注释模板.images\image-20220822105246690.png)

## 模板内语法

```java
** 
 * @Desc: $description$
 * @Date $date$ $time$
$params$ 
 * @return $returns$
*/
```

## 点击Edit variables

### param处填入以下代码

```groovy
groovyScript(
    "
    def result = ' * @params:';
    def params = \"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList();
    def type = \"${_2}\".split(',').toList();
    if(params[0]!=''){
        result+='\\r\\n ';
    };
    for(i = 0; i < params.size(); i++) {
        if(params[i] != ''){
            if(i==0){
                result+='	* @param '  + params[i] + ' ' + type[i] ;
                if(params.size()!=1){
                    result+=': \\r\\n '
                }
            }else{
                if(i<params.size()-1){
                    result+='	* @param '  + params[i] + ' [' + type[i] + ']' + ': \\r\\n ';
                }else{
                    result+='	* @param '  + params[i] + ' [' + type[i] + ': ';
                }
            }    
        }
    };
    return result",methodParameters(),methodParameterTypes()) 
```

### return处的代码（使用idea内置的方法也可以）

```groovy
groovyScript("return \"${_1}\" == 'void' ? null : '\\r\\n * @return ' + \"${_1}\"", methodReturnType()) 
```

![image-20220822105731802](E:\Note\Java\Idea方法注释模板.images\image-20220822105731802.png)

## 成果

![image-20220822105802489](E:\Note\Java\Idea方法注释模板.images\image-20220822105802489.png)