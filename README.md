#pl-sql-doc-generator
Generate Markdown documentation from pl/sql source code

This script generates markdown file from pl/sql source code.  
Get comments from package specification and transform it to markdown.  

##Before run
- Replace LIST_OF_PACKAGE_NAMES parameter to list of package names
`LIST_OF_PACKAGE_NAMES` -> 'MY\_MAIN\_PACKAGE', 'MY\_FUNCTIONS'
- Replace ./README_OUT.md to correct file path

##Rules
- comments starts from words  
`$pkg:` - name of package  
`$obj_type:` - type of code element like _function_, _type_, _procedure_  
`$obj_name:` - name of code element  
`$obj_desc:` - description. what does this element do?  
`$obj_param:` - parameter names and parameter description  
`$obj_return:` - description of return values  

- row starts from this words at first column. It's mean not from space, tab or smth else.  
    

- use `/*` and `*/` to comment block

example:

```
/*  
$pkg: MY_FUNCTIONS  
*/  

/*  
$obj_type: function  
$obj_name: square  
$obj_desc: calculate square of item and check is it a quadrate  
$obj_param: p_item(clob): is not null. json {  
$obj_param: p_item(clob):   x(number) is not null - height
$obj_param: p_item(clob):   y(number) is not null - length
$obj_param: p_item(clob): }  
$obj_param: o_error(varchar2(4000)): is null. output parameter. error message  
$obj_return: sys_refcursor {  
$obj_return:   square(number) is not null - value of square
$obj_return:   is_quadrate(varchar2(1)) is not null - flag Y/N. Is it quadrate?  
$obj_return: }  
*/  
```


- to generate file run this  
`sqlplus user/pass@server/db @./path/to/file`  
but make sure you set correct `./README_OUT.md` path

- at Sql Developer you can run just `@./path/to/file`  
but make sure you
set correct `Preferences->Database->Worksheet->Select default path to look for scripts` path  
