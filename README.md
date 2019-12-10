#　https://www.zhihu.com/question/19568896 主流开源协议之间的异同


### 一、制作首页App组件
1、完成Header区域，使用的是Mint-UI中的Header组件

2、制作底部的Tabbar区域，使用的是mui中的Tabbar组件

  2.1  先把扩展图标的css样式拷贝到项目中，根据错误提示导入相应的扩展包

3、要在中间区域放置一个router-view来展示路由匹配到的组件

4、创建路由实例对象后，把tabbar的a标签改成router-link标签
5、制作Tabbar的组件，设置成路由

6、在main.js中导入Tabbar组件，在路由对象中绑定路由

7、制作切换Tabbar的动画

### 二、制作首页轮播图
1、轮播图使用Mint-UI中的swipe组件

2、 获取数据，使用vue-resouce获取数据

### 三、使用mui制作首页的6宫格并且改造样式
1、改造图标，导入自己的图片

2、改造成路由并配置路由规则


### 四、首页的新闻资讯改造成路由
1、相应的样式的修改

2、时间格式化

3、新闻资讯列表改造成路由，实现点击跳转到新闻详情

4、把列表的每一项改造成router-link，同时，在跳转时提供唯一的id标示符


### 五、创建新闻详情的组件页面
1、实现新闻详情页的布局

2、单独封装一个comment.vue组件

  2.1  先创建一个单独的comment.vue组件模板

  2.2  在需要使用comment组件的页面中，先手动导入comment组件（import comment from ''）

  2.3  在父组件中，使用components属性，将刚才导入的comment组件，注册为自己的子组件

  2.4  将注册子组件的时候，注册名称，以标签形式在页面中引用即可

3、获取评论

  getComments()

4、加载更多

  4.1  为“加载更多”按钮绑定点击事件，请求下一页的数据

  4.2  点击“加载更多”，让pageIndex++，然后重新调用this.getComments();方法重新获取最新一页的评论

  4.3  为了防止新评论覆盖老评论，应该在加载更多的时候，每当获取新数据都应该拼接在后面


5、发表评论(遇到一个问题：发表之后可以看到新增的楼层，但是内容不显示，需要重新刷新才能看到评论内容)

   5.1  把数据框做双向数据绑定，为发表按钮绑定一个时间

   5.2  校验评论内容是否为空，如果为空，则用Toast提示用户，评论内容不能为空

   5.3  通过vue-resource发送一个请求，把评论内容提交给服务器
   
   5.4  当发表评论ok后，重新刷新列表，以查看最新的评论(如果调用getComments方法重新刷新列表的话，只能得到最后一页的评论，前几页的评论获取不到（原因是当评论加载出了2页或3页的时候，去调用getComments方法的时候，pageIndex就等于2或3，第一页的评论就get不到了）；换一个思路：当评论成功后，在客户端，手动拼接出一个最新的评论对象，然后调用数组的unshift方法，把最新的评论追加到data中的comments开头)
  

   ## 六、首页的图片分享改造成路由
   1、改造图片分享按钮为路由的链接并显示对应的组件页面

   2、绘制图片列表，组件页面结构并美化样式

    2.1 制作顶部的滑动条,使用MUI中的tab-top-webview-main.html，然后需要把slide区域的mui-fullscreen类去掉

    2.2 制作底部的图片列表

    2.3 滑动条无法正常触发滑动，通过检查官方文档，发现这是js组件，需要被初始化

    2.4 导入mui.js，调用官方提供的方式去初始化

    ---

    mui('.mui-scroll-wrapper').scroll({

      deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006

    });

    ---
    2.5 在初始化滑动条的时候导入的mui.js

     ### 移除webpack的严格模式

        1、安装移除严格模式的插件：npm install babel-plugin-transform-remove-strict-mode，然后在.babelrc文件下配
           
        置插件

        {
            "plugins": ["transform-remove-strict-mode"]
          }

     ### 遇到的问题：

          @1、引入mui的顶部滑动条之后，滑动条无法滑动

            解：刚进入图片分享页面的时候，滑动条无法正常工作，经过分析发现，如果要初始化滑动条，必须要等到DOM 元素加载
            
            完毕，所以把初始化滑动条的代码，放到mounted钩子函数里面。

          @2、底部的Tabbar无法切换

            解：app.vue组件里的router-link里的类mui-tab-item与mui自身冲突，修改这个类名为
            
            mui-tab-item-lib，把mui-tab-item类下相关的css样式都复制到mui-tab-item-lib下。

  3、制作图片列表区域

    3.1 图片列表使用懒加载技术，使用mint-ui提供的现成的组件"lazy load"

    3.2 实现点击图片跳转到图片详情页

        在改造li标签成router-link标签时，记得使用tag属性指定要渲染为哪种元素

    3.3 搭建出图片详情页的结构，评论部分使用已经写好的comment组件

    3.4 中间缩略图部分使用v-viewer插件
        先安装插件：npm i v-viewer  然后在main.js里导入包