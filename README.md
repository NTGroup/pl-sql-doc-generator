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
`$obj\_desc:` - description. what does this element do?  
`$obj_param:` - parameter names and parameter description  
`$obj_return:` - description of return values  

- row starts from this words at first column. It's mean not from space, tab or smth else.  
    

- use ```/*``` and ```*/``` to comment block

example:

```
/*  
$pkg: MY_FUNCTIONS  
*/  

/*  
$obj_type: function  
$obj_name: pnr_list  
$obj_desc: get pnr list whith id listed in p_pnr_list. written for NQT.  
$obj_param: p_pnr_list(t_clob): is not null. json {  
$obj_param: p_pnr_list(t_clob):   p_pnr_id(t_long_code) is not null - id from NQT. search perform by this id  
$obj_param: p_pnr_list(t_clob):   p_tenant_id(t_long_code) is not null - id of contract in text format, for authorization  
$obj_param: p_pnr_list(t_clob): }  
$obj_param: p_rownum(t_id): is null. filter for rows count. if null then fetch all rows
$obj_return: sys_refcursor {  
$obj_return:   pnr_id(t_long_code) - id from nqt  
$obj_return:   nqt_status(t_long_code) - name of task that scheduled by NQT and processed by PO  
$obj_return:   po_status(t_long_code) - progress status of task that scheduled by nqt  
$obj_return:   nqt_status_cur(t_long_code) - name of current task that scheduled by nqt  
$obj_return:   po_msg(t_msg) is null - equal NULL  
$obj_return:   item_type(t_long_code) is not null  - equal 'avia'   
$obj_return:   pnr_locator(t_long_code) - pnr locator code  
$obj_return:   tenant_id(t_long_code) - id of contract  
$obj_return: }  
*/  
```


- to generate file run this  
```sqlplus user/pass@server/db @./path/to/file```  
but make sure you set correct ```./README_OUT.md``` path

- at Sql Developer you can run just ```@./path/to/file```  
but make sure you
set correct ```Preferences->Database->Worksheet->Select default path to look for scripts``` path  
