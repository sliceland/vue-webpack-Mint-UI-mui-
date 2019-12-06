#　https://www.zhihu.com/question/19568896 主流开源协议之间的异同


## 一、制作首页App组件
# 1、完成Header区域，使用的是Mint-UI中的Header组件
# 2、制作底部的Tabbar区域，使用的是muui中的Tabbar组件
#   2.1  先把扩展图标的css样式拷贝到项目中，根据错误提示导入相应的扩展包
# 3、要在中间区域放置一个router-view来展示路由匹配到的组件
# 4、创建路由实例对象后，把tabbar的a标签改成router-link标签
# 5、制作Tabbar的组件，设置成路由
# 6、在main.js中导入Tabbar组件，在路由对象中绑定路由
# 7、制作切换Tabbar的动画

## 二、制作首页轮播图
1、轮播图使用Mint-UI中的swipe组件
2、 获取数据，使用vue-resouce获取数据

## 三、使用mui制作首页的6宫格并且改造样式
1、改造图标，导入自己的图片
2、改造成路由并配置路由规则


## 四、首页的新闻资讯改造成路由
1、相应的样式的修改
2、时间格式化
3、新闻资讯列表改造成路由，实现点击跳转到新闻详情
4、把列表的每一项改造成router-link，同时，在跳转时提供唯一的id标示符

## 五、创建新闻详情的组件页面
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
   5.1  把数据框做双向数据绑定
   5.2  为发表按钮绑定一个时间
   5.3  校验评论内容是否为空，如果为空，则用Toast提示用户，评论内容不能为空
   5.4  通过vue-resource发送一个请求，把评论内容提交给服务器
   5.5  当发表评论ok后，重新刷新列表，以查看最新的评论(如果调用getComments方法重新刷新列表的话，只能得到最后一页的评论，前几页的评论获取不到（原因是当评论加载出了2页或3页的时候，去调用getComments方法的时候，pageIndex就等于2或3，第一页的评论就get不到了）；换一个思路：当评论成功后，在客户端，手动拼接出一个最新的评论对象，然后调用数组的unshift方法，把最新的评论追加到data中的comments开头)

   ## 六、首页的图片分享改造成路由
   1、改造图片分享按钮为路由的链接并显示对应的组件页面