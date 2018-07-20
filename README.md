# PHPAutoword
适用于THINKPHP5框架 其他框架待完善
1. 安装：
直接执行:
```
composer require "lxclass/phpautoword"
```
或者修改composer.json文件
```
// 在require里加上
"lxclass/phpautoword": "0.*"
```
2. 使用方法

在 application/extra 目录下创建文件名为 documents_v1.php 的配置文件。 
```
//documents_v1.php非固定文件可在类包lxclass\phpautoword\src\Documents.php 文件
  自动加载函数 $this->config = Config::get('documents_v1'); 内修改
```
配置文件内容如下：
```
<?php
return [
    'title' => "XXXX公司",  
    'description' => '"XXXX" | APi接口文档等等。',
    'template' => 'grape', // 苹果绿:apple 葡萄紫:grape
    'class' => [
        'app\sms\controller\Handle'
        // ...
    ],
];
```
其中 template 为模板类型，暂时提供两种模板风格，分别为苹果绿(未完善)和葡萄紫，虽然两套模板都是巨丑无比。所以使用的过程中也可以自己开发模板。

**重点:** class 为将要生成文档的类(带命名空间)

2. 示例：

| 注释参数 | 含义 | 说明 |
| - | - | - |
| @title | 标题 | 文档生成的类方法标题 |
| @desc | 描述 | 格式如下，地址、请求方式、备注等 |
| @param | 接收参数 | 格式如下，name:名称、type:类型、required:是否必须、default:默认值、desc:说明 |
| @paramcode | 接收参数示例 | 代码块 |
| @return | 返回参数 | 格式如下，name:名称、type:类型、required:是否必须、desc:说明、level：层级 |
| @showcode | 返回参数示例 | 代码块 |

类的具体实现方法：

```
<?php
/**
 * @authors Lx (you@example.org)
 * @date    2018-06-30 14:12:34
 * @version $Id$
 */

namespace app\sms\controller;
use think\Controller;
use think\Db;

class Handle extends Controller {

	public function __construct(){
    }


    //创建短信模版
    /**
     * @title 创建短信模版
     * @desc  {"0":"接口地址：handle/createSmsTem","1":"请求方式：POST","2":"应用场景：创建短信模版 营销模版创建完毕后需提交模版请向短信平台报备 验证码模版不需要"}
     * @param {"name":"content","type":"int","required":true,"default":"","desc":"短信内容参数请用‘{param}’表示"}
     * @param {"name":"type","type":"int","required":true,"default":"","desc":"短信类型 1为验证码短信 2为营销普通短信"}
     * @paramcode {"content":"【{param}】 您的验证码是{param}。请在页面中提交验证码完成验证。","type":"模版添加成功","type":1}
     * @return {"name":"code","type":"int","required":true,"desc":"返回码：200模版添加成功 201请求参数错误 202异常错误，请联系管理员","level":1}
     * @return {"name":"msg","type":"string","required":true,"desc":"返回信息","level":1}
     * @return {"name":"data","type":"array","required":true,"desc":"数据","level":1}
     * @return {"name":"templateId","type":"int","required":true,"desc":"短信模版ID","level":2}
     * @showcode {"code":"200","msg":"模版添加成功","data":{"templateId":"400003"}}
    */
    public function createSmsTem($value='')
    {
      你的代码块
    }
```

编辑好配置文件之后 直接打开浏览器访问 http://localhost/api/documents 即可看到文档页。

未完待续
