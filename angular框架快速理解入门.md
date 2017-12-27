# 首先大家知道Angular是由Google公司开发维护的前端MVC框架，那么什么叫做MVC框架呢
 > 1. MVC是一种由后端带入前端的一种开发模式，主要是为了降低代码耦合度（就是什么类型代码都在一起）
 > 2. MVC是由，Model（模型），View(视图)，controller（控制器）三部分组成
   - M（模型一般就是处理数据的，操作数据库）
   - V（视图一般就是展示数据的，通过HTML展示）
   - C（控制器就是连接模型和视图的）
## 那为什么有人说angular是MVVC框架呢，其实就是因为它的双向数据绑定$scope
  View不能直接与Model交互，而是通过$scope这个ViewModel来实现与Model的交互   
## 先来说说angular，因为我用的是angular1的版本所以您就将就下
> 1. 首先说说Angular是一个JS框架大家应该知道的。它可以通过<script>标签添加到HTML页面
> 2. 再来说说它的优缺点
<pre>
优点
{
   > 1. 模版功能强大丰富，自带丰富的Angular指令
   > 2. 是一个比较完善前端MVC框架，包括模版，数据双向绑定，路由，模块化，服务，过滤器，
     依赖注入功能；
   > 3. 自定义指令，比较灵活满足大多数的需求
   > 4. ng模块化比较大胆的引入java中的东西（就是依赖注入）使代码复用性强      
 }
 </pre>
 <pre>
 缺点
  ｛
    > 1. 验证功能错误信息显示比较薄弱，需要写很多模版标签
    > 2. Angular太笨重了，没有让用户选择一个轻量级的版本，当然1.2以后的版本有一些改动，把route animate
     模块独立了出去
    > 3. 这次从1.0升级到2.0版本，改动特别大，没有完美兼容低版本，升级后可能会导致一个兼容新的bug
   ｝
  </pre> 
## 下面就开始开始angular的旅程
> 1. 定义应用是使用angular的开始通过给HTML页面上的标签添加ng-app属性，它所包裹的范围都属于此应用
 例如：<html lang='en' ng-app='app'>表示整个页面文档都为此应用区域
> 2. 定义模块：利用Angular提供的全局对象angular中的方法，angular-module()来定义一个模块
  //angular.module()其中第一个参数是定义的模块名称，第二个参数是准备依赖的模块
 例如：var app = angular.module('app',[])
> 3. 定义控制器：
 控制器（Controller）作为连接模型（Model）和视图（View）的桥梁存在，所以当我们定义好了控制器以后也就定义好了模型和视图。
 例如：app.controller('控制器名称（用英文）'，['$scope'，function()}])
## angular中的内置指令 
<pre>	
ng-app 指定应用根元素，至少有一个元素指定了此属性。
ng-init 初始化一个Angular应用程序的数据
ng-model 指令定义在AngularJS应用中使用的模型/变量
ng-repeat遍历元素集合
ng-bind 绑定数据到视图层
ng-controller 指定控制器
ng-click 单击事件
ng-dbclick双击事件
ng-blur失去焦点
ng-show控制元素是否显示，true显示、false不显示
ng-hide控制元素是否隐藏，true隐藏、false不隐藏
ng-if控制元素是否“存在”，true存在、false不存在
ng-src增强图片路径
ng-href增强地址
ng-class控制类名
ng-include引入模板
ng-disabled表单禁用
ng-readonly表单只读
ng-checked单/复选框表单选中
ng-selected下拉框表单选中
</pre>
## angular中强大的自定义指令可以帮你增添便利
### angular中根据实际业务需要自定义指令，通过angular全局对象下的directive方法实现
<pre>	
语法格式：
   var app  = angular.module('app',[]);
   //tag位置可以写自己定义的指令名称
   app.directive('tag',function(){
     return{
       //自定义指令类型 E C M A 
       E(元素)
       C(样式类)
       M(注释类)
       A(属性类)
       //表示自定义的指令可以用以上类型加到html中
       restrict:'ECMA',
       //是否替换标签,默认是false这里你就记住写true把，他会把你自定义的指令标签替换掉
       replace:true,
       //指令模版
       template：'可以是任何东西、标签、函数，或者页面'

     }
   })
</pre>   
## 数据绑定angularjs中的重点之一
> 1. 提到绑定就要想到的（ng-bind、ng-model、{{}})
> 2. 其中ng-bind和{{}}都是绑定数据用的，{{}}是ng-bind的简写，通过“{{}}”绑定数据时会
有“闪烁”现象，添加ng-cloak也可以解决“闪烁”现象，通过ng-bind-template可以绑定多个数据。
> 3. 通过表单元素添加ng-model指令实现视图（View）模版向模型（Model）数据绑定
<pre>
  <!DOCTYPE html>
 <html lang="en" >
 <head>
    <meta charset="UTF-8">
    <title>Document</title>
 </head>
 <body ng-app="app" >
    <div ng-controller="controller">
        <input type="text"  placeholder="nihao" ng-model="name">
        <p ng-bind="name"></p>
        <p>{{name}}</p>
    </div>
    <script src="angular.min.js"></script>
    <script>
        var app = angular.module("app",[]);
        app.controller("controller",["$scope",function($scope){
            $scope.name="";
        }])

        //angular 1.3版本之后就不支持全局控制器了
        // function controller($scope){
        //     $scope.name=''
           
        // }
    </script>
 </body>
 </html>
</pre>
## Angular中的作用域
简单来说就是app不能嵌套controller可以嵌套，每个控制器（Controller）又都对应一个模型（Model）也就是$scope对象，
不同层级控制器（Controller）下的$scope便产生了作用域。

### 根作用域
一个AngularJS的应用在启动时会自动创建一个根作用域$rootScope，这个根作用域在整个应用范围（ng-app所在标签以内）都可以访问
//ng-init可以为根作用域添加数据，这个数据在此app范围下都能访问到
<pre>
<div ng-app="app" ng-init="name='wbj'">
    <p>{{name}}</p>
</div>
</pre>
### 子作用域
通过ng-controller指令可以创建一个子作用域，新建的作用域可以访问其父作用域的数据

## 过滤器
在AngularJS中使用过滤器格式化展示数据，在"{{}}"中使用“|”来调用过滤器，使用“：”传递参数

### 内置过滤器
<pre>
1.currency将数值格式化为货币格式
 <p>{{12|currency:'￥'}}</p>
2.date 日期格式化
年（y）、月（M）、日（d）、星期（EEEE/EEE）、时（H/h）、分（m）、秒（s）、毫秒（.sss），也可以组合到一起使用
 <p>{{date|date:'yyyy-MM-dd hh:mm:ss'}}</p>
 //用这个日期格式话的时候一般都有时间更新就用到了angular的脏检查机制
 //使用$apply()方法进入angular context然后通过$digest触发脏检查
 //angular的脏检查就会涉及双向绑定内部机制了想了解的私聊我QQ：929364695
   setInterval(function(){
                $scope.$apply(function(){
                $scope.date= new Date();
            })
            },1000)
3.filter在给定数组中选择满足条件的一个子集，并返回一个新数组，其条件可以是一个字符串、对象、函数
 html中：<p>{{ch| filter : 'a'}} </p>
 angular中：$scope.ch= [
            {name:'kimi',age:3},
            {name:'cindy',age:4},
            {name:'anglar',age:4},
            {name:'shitou',age:6},
            {name:'tiantian',age:5}
            ];
4.json将Javascript对象转成JSON字符串
 {{ jsonTest | json}}
5.limitTo取出字符串或数组前（正数）几位或后（负数）几位
 {{ childrenArray | limitTo : 2 }} //将会显示数组中的前两项
6.lowercase将文本转换成小写格式
7.uppercase将文本转换成大写格式
8.number数字格式化，可控制小位位数
 {{ num | number : 2 }}
9.orderBy对数组进行排序，第二个参数可控制方向
 { 数组 | orderBy : 自己指定 }}
</pre>
### 自定义过滤器
<pre>
除了使用AngularJS内建过滤器外，还可以根业务需要自定义过滤器，
通过模块对象实例提供的filter方法自定义过滤器。
 app.filter('自定义名称',function(){
    return function(定义形参接收数据){
      return 处理好的数据
    }
 })
</pre>
## 依赖注入功能；
> 1. Angular采用模块化的方式组织代码，将一些通用逻辑封装成一个对象或者函数，实现最大程度上的复用
 这导致了使用者和被使用者之间存在依赖关系
> 2. 所谓依赖注入是指在运行时自动查找依赖关系，然后将查找到依赖传递给使用者的一种机制
> 3. 常见的angularjs内置服务有$http、$location、$timeout、$rootScope等
### 推断是注入（不推荐）
<pre>
//没有明确声明依赖，AngularJS会将函数参数名称当成是依赖的名称
 app.controller('demoController',function($http){
  $http({
    method:'post',
    url:'xx.php',
    data:{}
  })
 })
  这种方式带来的一个问题，当代码经过gulp压缩之后函数参数也被压缩，这样就会造成无法依赖
</pre>  
### 行内注入(推荐)
<pre>
以数组形式明确声明依赖，数组元素都是包含依赖名称的字符串，数组最后一个元素是依赖注入的目标函数
 app.controller('hangneiComtroller',['$http',function($http){
   $http({
     method:'post',
     url:'xx.php',
     data:{}
   })
 }]) 
</pre>
## 服务
服务是一个对象或者函数，对外提供特定的功能
### 内置服务
<pre>
> 1.$location是对原生Javascript中location对象属性和方法的封装
 app.controller('demoController',['$scope','$location',function($scope,$location){
   //绝对路径
   $scope.absUrl = $location.absUrl();
   //协议
   $scope.protocol = $location.protocol();
   //端口
   $scope.port = $location.port();
   //获取当前url的子路径(也就是当前url#后面的内容,不包括参数):
   $scope.path = $location.path();
   //获取当前url的哈希值
   $scope.hash = $location.hash();
   //设置或返回从问号 (?) 开始的 URL（查询部分）
   $scope.search = $location.search();
 }]) 

 > 2. $filter在控制其中格式化数据(鸡肋用不上)
   app.controller('demoController',['$scope','filter',function($scope,$filter){
     //原始信息
     $scope.content = 'my name is WBJ ';
    //创建过滤器
    var uppercase = $filter('uppercase');
    //格式化数据
    $scope.content = uppercase($scope.content);
   }])

 > 3.$timeout和$interval对原生js中的setTimeout和setInterval进行了封装
   app.controller('demoController',['$scope','$timeout','$interval',function($scope,
   $timeout,$interval){
     $timeout(function(){
       $scope.time = new Date();
     },1000);
     $interval(function(){
       $scope.time = new Date();
     },1000)
   }]) 

>  4.$log打印调试信息
  //启用日志服务
  app.controller('demoController',['$scope','$log',function($scope,$log){
    $log.log('日志');
    $log.info('信息');
    $log.warn('警告');
    $log.error('错误');
    $log.debug('调试')；
  }]) 

 > 5.$http用于向服务器发起异步请求（重点）
  //使用$http服务
  app.controller('demoController',['$scope','$http',function($scope,$http){
    //发起异步请求
    $http({
      method:'post',//请求方式
      url：'xx.php',//请求地址
      data:{name:'wbj',age:10},
      headers:{
         //请求头信息
         'Content-Type':'application/x-www-form-urlencoded'
      }
    }).success(function(data,status,headers,config){
        //响应成功
    })error(function(data,status,headers,config){
        //处理响应失败
    })
  }])
</pre>
## 自定义服务
通过上面例子得知，所谓服务是将一些通用性的功能逻辑进行封装方便使用，
AngularJS允许将自定义服务。
1.factory方法作用就是返回一个有属性有方法的对象
 <!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="anglar.min.js"></script>
</head>
<body>
<div ng-app="myApp" ng-controller="myCtrl">
    <p>{{r}}</p>
</div>

<script>
    //创建模型
    var app = angular.module('myApp', []);

    //通过工厂模式创建自定义服务
    app.factory('myFactory', function() {
        var service = {};//定义一个Object对象'
        service.name = "张三";
        var age;//定义一个私有化的变量
        //对私有属性写getter和setter方法
        service.setAge = function(newAge){
            age = newAge;
        }
        service.getAge = function(){
            return age; 
        }
        return service;//返回这个Object对象
    });
    //创建控制器
    app.controller('myCtrl', function($scope, myFactory) {
        myFactory.setAge(20);
        $scope.r =myFactory.getAge();
        alert(myFactory.name);
    });
</script>
</body>
</html>

2.通过service方式创建自定义服务，相当于new的一个对象,
只要把属性和方法添加到this上才可以在controller里调用。
//自定义服务显示日期
 app.service('showTime',['$filter',function($filter){
    var now = new Date();
    this.now = $filter('date')(now,'yyyy/MM/dd');
 }])
//声明依赖调用服务
app.controller('demoController',['$scope','showTime',function($scope,$showTime){
  $scope.now = showTime.now;
}])

3.value方法定义常量
app.value('服务名'，'对应的常量值')

4.provder方法如果想在 service 对象启用之前，先进行模块范围的配置，那就应该选择 provider
 
   //需要注意的是：在注入provider时，名字应该是：providerName+Provider   
    app.config(function(myProviderProvider){
        myProviderProvider.setName("大圣");       
    });
    app.provider('myProvider', function() {
        var name="";
        var test={"a":1,"b":2};
        //注意的是，setter方法必须是(set+变量首字母大写)格式
        this.setName = function(newName){
            name = newName  
        }

        this.$get =function($http,$q){
            return {
                getData : function(){
                    var d = $q.defer();
                    $http.get("url")//读取数据的函数。
                        .success(function(response) {
                            d.resolve(response);
                        })
                        .error(function(){
                            d.reject("error");
                        });
                    return d.promise;
                },
                "lastName":name,
                "test":test
            }   
        }

    });
    app.controller('myCtrl', function($scope,myProvider) {
        alert(myProvider.lastName);
        alert(myProvider.test.a)
        myProvider.getData().then(function(data){
            //alert(data)
        },function(data){
            //alert(data)
        });
    });

###配置块
通过config方法实现对模块的配置，AngularJS中的服务大部分都对应一个“provider”，
  用来执行与对应服务相同的功能或对其进行配置。
  比如$log、$http、$location都是内置服务，相对应的“provider”分别是
   $logProvider、$httpProvider、$locationPorvider。
  实例：log的
  app.config(['$logProvider',function($log){
    $log.debugEnabled(false);
  }])
###运行块
服务也是模块形式存在的对且对外提供特定功能，前面学习中都是将服务做为依赖注入进去的，
然后再进行调用，除了这种方式外我们也可以直接运行相应的服务模块，AngularJS提供了run方法来实现
app.run(['$http','$rootScope',function($http,$rootScope){
  $http({
    method:'post',
    url:'xx.php',
  }).success(function(data){
    $rooScope.name = data;
  })
}])
不但如此，run方法还是最先执行的，利用这个特点我们可以将一些需要优先执行的功能通过run方法来运行，
比如验证用户是否登录，未登录则不允许进行任何其它操作。
##路由（写了这么久终于到路由了）
一个应用是由若个视图组合而成的，根据不同的业务逻辑展示给用户不同的视图，路由则是实现这一功能的关键。
###SPA
  SPA（Single Page Application)指的是单一页面展示所有功能，通过Ajax动态获取数据然后进行实时渲染，
结合CSS3动画模仿原生App交互，然后再进行打包（使用工具把Web应用包一个壳，这个壳本质上是浏览器）变成一个“原生”应用。
  在PC端也有广泛的应用，通常情况下使用Ajax异步请求数据，然后实现内容局部刷新，局部刷新的本质是动态生成DOM，
  新生成的DOM元素并没有真实存在于文档中，所以当再次刷新页面时新添加的DOM元素会“丢失”，通过单页面应可以很好的解决这个问题。
###路由 
 1. 在后端开发中通过URL地址可以实现页面（视图）的切换，但是AngularJS是一个纯前端MVC框架，在开发单页面应用时，所有功能都在同一页面完成，所以无需切换URL地址（即不允许产生跳转），
  但Web应用中又经常通过链接（a标签）来更新页面（视图），当点击链接时还要阻止其向服务器发起请求，通过锚点（页内跳转）可以实现这一点。
   实现单页面应用需要具备：
    a、只有一页面
    b、链接使用锚点

2.单一页面中可以能过hashchange事件监听到锚点的变化，进而可以实现为不同的锚点准不同的视图，
  单页面应用就是基于这一原理实现的。
  AngularJS对这一实现原理进行了封装，将锚点的变化封装成路由（Route）,这是与后端路由的根本区别
####使用方法
1.引入angular-route.js(注意先引angular.js)  
 //Angular核心
 <script src="angular.min.js"></script>
 //引入路由模块
 <script src="angular-route.js"></script>
 2.实例化模块（app)时，当成依赖传进去（模块名称叫ngRoute)
 var app = angular.module('app',['ngRoute']);

 3.配置路由模块
 //通过routeProvider
 app.config('$routeProvider',function($routeProvider){
   //配置路由 
   $routeProvider.when('/',{
     template:'起名字'
   })
 })
 
 4布局模版：ng-view是占位用的路由配置的视图会被加载到相应位置
 通过ng-view指令布局模板，路由匹配的视图会被加载渲染到些区域。
  <div ng-view></div>
###路由参数
1、提供两个方法匹配路由，分别是when和otherwise，when方法需要两个参数，otherwise方法做为when方法的补充只需要一个参数，其中when方法可以被多次调用。
2、第1个参数是一个字符串，代表当前URL中的hash值。
3、第2个参数是一个对象，配置当前路由的参数，如视图、控制器等。
	a、template 字符串形式的视图模板
	b、templateUrl 引入外部视图模板
	c、controller 视图模板所属的控制器
	d、redirectTo跳转到其它路由

##补充
jquery:在没有引入jQuery的前提下AngularJS实现了简版的jQuery Lite，通过angular.element不能选择元素，
  但可以将一个DOM元素转成jQuery对象，如果引提前引入了jQuery则angular.element则完全等于jQuery。
###Angular常遇到的问题
Q1.<div ng-include="views/user/show.html"></div> 错在哪里？
如果你这么写过，会发现这个位置啥也没有加载出来，那么，错在哪里呢？错在ng-include需要的是一个变量，
如果你在$scope中有这样一个变量 $scope.userShowTemplateUrl = "views/users/show.html"，并且把上面这句变为<div ng-include="userShowTemplateUrl"></div>就能正常工作了。
或者这样写也行：<div ng-include=" 'views/user/show.html' "></div>

原因何在？

因为在ng-include中，是把它的参数当做变量来解释的，它会通过$eval对传入的值进行计算，然后作为模板地址去加载。
不过，更好的方法是把这些界面片段（partical）写成指令，那样你就不用在多处重复写路径了，更重要的是，将来你可以直接在这里扩展它的交互逻辑，从界面原型平滑的演化到线上系统。

Q2. 我的指令怎么无效？
如果你排除了代码错误等问题，那么最可能的原因是restrict。restrict参数是用来规定你可以通过哪种方式来使用指令，而这个问题之所以容易成为坑，是因为restrict的默认值是A，
也就是说，默认情况下，指令只能通过属性的形式使用，比如我写了一个指令叫做appHeader，那么默认情况下我只能用这样的形式使用它：<div app-header></div>，而<app-header></app-header>的形式则是无效的。

Q3. 修改了变量怎么界面没反应？
首先你当然要检查有没有错误以及是否确实是scope变量，如果这些都没问题，那么多半儿是$apply导致的。
对于大多数操作，$apply都会自动执行，所以你不用担心，但是如果你使用了angular之外的功能，
比如直接调用了setTimeout函数、挂接了jquery的事件、使用了jquery的ajax操作等等，那么系统就没有机会帮你调用$apply，界面也就没有机会刷新了，
但是你如果之后又做了其他会导致$apply的操作，你会发现以前“欠下”的那次界面刷新被正常执行了了 …… 迟到的刷新仍然是bug。

##学到这估计大家都会了解了angular，大家去多练习把！（没事也打开我保存的图片看看没准就有你疑惑的地方）

  


