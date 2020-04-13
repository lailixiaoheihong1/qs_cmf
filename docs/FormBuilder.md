## FormBuilder

#### 事件
+ startHandlePostData   
确定按钮会监听该事件类型，可传递一个按钮描述。触发该事件后确定按钮会无效，描述会改成传递的字符串。
+ endHandlePostData  
确定按钮会监听该事件类型，触发该事件，确定按钮会重新生效，按钮描述会恢复。

#### ueditor
指定上传文件的url格式采用包含域名的url格式（默认采用相对url路径）
```php
//addFormItem第七个参数，传递指定的上传处理地址，加上urldomain参数，设为1
->addFormItem('desc', 'ueditor', '商家简介', '', '', '', 'data-url="/Public/libs/ueditor/php/controller.php?urldomain=1"')
```

使用oss作为文件存储服务
```php
//addFormItem第七个参数，传递指定的上传处理地址, oss设为1表示开始oss上传处理，type为指定的上传配置类型
->addFormItem('content', 'ueditor', '正文内容','', '','','data-url="/Public/libs/ueditor/php/controller.php?oss=1&type=image"')
```

复制外链文章时，强制要求抓取外链图片至本地，未抓取完会显示loadding图片(默认也会抓取外联图片，但如果未等全部抓取完就保存，此时图片还是外链)
```php
//addFormItem第七个参数，设置data-forcecatchremote="true"
->addFormItem('desc', 'ueditor', '商家简介', '', '', '', 'data-forcecatchremote="true"')
```

设置ue的option参数
```php
//如：想通过form.options来配置ue的toolbars参数
//组件会自动完成php数组--》js json对象的转换，并传入ue中
->addFormItem('content', 'ueditor', '内容', '', ['toolbars' => [['attachment']]])
```

自定义上传config设置

```blade
在app/Common/Conf 下新增ueditor_config.json或者ueditor_config.php(返回数组)，该文件将会替换掉默认的config.json。如有客制化config.json的需求，定制该文件即可。
```

#### addFormItem
```blade
该方法用于加入一个表单项

参数
$type 表单类型(取值参考系统配置FORM_ITEM_TYPE)
$title 表单标题
$tip 表单提示说明
$name 表单名
$options 表单options
$extra_class 表单项额外样式，如使用hidden则隐藏表单
$extra_attr 表单项额外属性
$auth_node 字段权限点，需要先添加该节点，若该用户无此权限则unset该表单；格式为：模块.控制器.方法名，如：['admin.Box.allColumns']

若auth_node存在多个值，则需要该用户拥有全部权限才会显示该表单

```