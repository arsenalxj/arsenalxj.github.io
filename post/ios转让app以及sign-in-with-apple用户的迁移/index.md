# 关于iOS转让App以及Sign In With Apple用户的迁移


​	前段时间在处理iOS转让App的事情，看了苹果官方的文档和网上一些文章，对整个流程有了大体的了解，但是还是有一些点不是很清楚。经过多方求证和实际操作，记录一下。

流程啥的不说了，可以参考以下链接，这里只记录一些点。

[iOS APP 转让避坑指南 - 掘金 (juejin.cn)](https://juejin.cn/post/7140823445423521806)

[iOS App的转让/迁移和接收流程 - 简书 (jianshu.com)](https://www.jianshu.com/p/f598ae3f78ed)

[iOS，Sign in with apple transfer - 简书 (jianshu.com)](https://www.jianshu.com/p/aad66d49553e)



#### 在新账号那边点击接受后，多久能完成转让

在网上看的文章，有些说很快，有些说要等一两天。实际操作后，我这边是马上生效的，应该是没有审核的。在旧账号那边点击转让，马上就能在新账号那边看到，点击接受后，马上就生效了。



#### 转让完成后，玩家通过Sign In With Apple登录获取到 identifier 值

这个值在转让完成后，立刻就会改变。如果不做用户迁移的工作，用户会找不回来之前的账号。我们为了不影响用户，是做了次停服。



#### 为玩家转换得到新的 identifier，这个过程有没有办法测试

据我了解是没有的，我们最终也没有测试，只能说是相信苹果。

转换的过程分两步：旧的identifier -> 中间值 -> 新的identifier

第一步 [Transferring your apps and users to another team | Apple Developer Documentation](https://developer.apple.com/documentation/sign_in_with_apple/transferring_your_apps_and_users_to_another_team/)

第二步 [Bringing new apps and users into your team | Apple Developer Documentation](https://developer.apple.com/documentation/sign_in_with_apple/bringing_new_apps_and_users_into_your_team)

第二步只能在转让App完成后执行，因为需要一个key，而这个key要在转让完成后才能生成。我看网上有些人好像可以提前创建app来获取这个key，这个我不懂怎么操作。

所以第二步无法测试。

这里还有一点，一般旧的identifier都有三段，类似 xxx.xxx.xxx 这样的结构，第一步得到的中间值只有两段，xxx.xxx，这个跟苹果文档里面的不一样，一度怀疑是不是我们搞错了。最后得不到答案，只能硬着头皮上了。

还有，我们实际执行过程中，发现请求接口的速度过慢，应该是苹果那边做了频率限制，我们就开多了几个进程去跑，就快了很多。




