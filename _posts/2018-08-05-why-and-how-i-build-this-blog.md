---
category: tech
tags: blog github-pages jekyll minimal-mistakes staticman
---

# Why

高中时曾用WordPress做过一个blog，存粹是由于新奇和好玩，但当时没有记录的意识，~~毕竟写作文就够让我头疼了:speak_no_evil:~~

上了大学后接触的知识逐渐多起来，明显感觉到很多东西用的时候很熟练，但一段时间不用就会忘掉，这时候又得重新四处找资料学习一遍，于是逐渐萌生了整理记录知识的念头。

而真正的导火索是我的《操作系统》老师姜奶奶说的一句话：“你们天天上网看别人的博客，别人写他这个bug是怎么解决的，写的挺好，但为什么写的这个人不是你呢？”

一语惊醒梦中人

于是决定这个暑假要把自己的博客建起来。既能提高自己的写作水平，更能将自己记录下来的知识与别人分享。

下面就简单说说我建这个博客的相关技术、大概流程和遇到的某些具体问题

# How

本博客依托于Github-Pages，使用Jekyll搭建，主题是Minimal Mistakes，评论系统使用Staticman_v2。

如何一步步的搭建，[Github-Pages的doc](https://pages.github.com/)、[Jekyll的doc（中文）](https://jekyllcn.com/docs/home/)、[Jekyll的doc（英文）](https://jekyllrb.com/docs/home/)、[Minimal Mistakes的doc](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)都写的挺详细的，可能一下子还有些地方看不太懂，可以搭配着看看[别人写的建站博客](https://www.google.com/search?q=github+pages+jekyll+%E5%BB%BA%E7%AB%99)。

静态博客的评论系统可以自己写一个，也可以使用第三方的：[第三方评论系统推荐 • 水八口记](https://blog.shuiba.co/comment-systems-recommendation)，[如何评价「多说」即将关闭？有什么替代方案？ - 知乎](https://www.zhihu.com/question/57426274)，我使用的[Staticman_v2](https://staticman.net/)会将评论存到本博客的repo里。

在此想着重记录一下我在建站过程中的几个问题

1. 有关主题的配置

    * Github-Pages有推荐的几个Jekyll主题，在[这个文档](https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site-with-the-jekyll-theme-chooser/)里可以看到如何使用Theme Chooser选择一个它推荐的主题，新建repo的时候如果名字是[自己的用户名].github.io好像也会让你选择主题。

    * 如果觉得这几个主题都丑（比如我），可以使用开源的主题，在_config.yml里有一项`remote_theme`，它的值设为开源主题的所有者/repo的名字，例如`remote_theme: "mmistakes/minimal-mistakes"`。并且需要将`theme`这项注释掉，否则每push一次（也就是Jekyll重新部署一次）github会给你发一个邮件

        >The page build completed successfully, but returned the following warning for the `master` branch:<br>
        >You are attempting to use a Jekyll theme, "minimal-mistakes-jekyll", which is not supported by GitHub Pages......
    
    * 也可以自己写sass，也就相当于使用非开源的主题，`remote_theme`这项就应该空着。

2. 有关Staticman的配置

    * staticman.yml就照着配置就行了，注意_config.yml里一定要设置好三个参数：repository、comments.provider、staticman.branch

    * `path: "_data/comments/{options.slug}"`这个path一定不能以/开头啊，我是参照[minimal-mistakes的文档](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#configure-staticman)修改的，它的blog是放在docs目录里的，所以[它的path](https://github.com/mmistakes/minimal-mistakes/blob/master/staticman.yml#L86)前面是docs/，这里的示例我估计是它为了改成一般人的情况，但少删除了一个/，我测试评论的时候怎么也不成功，看了这部分的代码(_includes/comments-providers/staticman_v2.html)，失败会`console.log(err)`，于是打开F12，看报错信息。我测试了很多次，前几次是报错`Too many requests in this time frame.`，让我过10分钟再试，可是再测试还是报同样的错，多试了几次后，错误变成了`Unprocessable Entity`，错误代码是`"GITHUB_WRITING_FILE"`，并且告诉了我是slash的问题，这才解决...

    * `filename: "{@date:YYYY-MM-DD}-{fields.name}"`这是我之前的filename的配置，是不对的。因为每一次评论都会产生一个文件，文件名按照这个filename的规则生成，如果同一个name的评论者在同一天内评论两遍，就会造成文件名相同，如图所示：![](https://i.loli.net/2018/08/05/5b66018f9e94b.png)

    * reCaptcha得到的secret key要记得[使用这个加密](https://staticman.net/docs/encryption)再填进去哟，因为我们的配置文件都是在github上开源的，别人会直接看到内容，ps:评论的email也是md5转换过再存文件的

大概就是这些吧~有什么问题都可以评论交流哟~

说句题外话：千万不要撒谎，珍惜别人给予的信任