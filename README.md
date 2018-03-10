# CustomedKeyboardDemo

从前，公司有个需求，要我写个键盘登录用。
两三天之后，它就出来了。但是没多久，这个需求又被砍了。。。

![键盘截图.png](http://upload-images.jianshu.io/upload_images/1794486-abebe9040c7af76d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 简单介绍

- 使用autolayout布局，block回调。
- 样式参照工商银行的键盘布局。
- 键盘分三种输入类型：
    - 字母
    - 数字（每次切换均为随机乱序）
    - 符号
- 该键盘输入的内容为密文（非系统的密文模式），输入内容保存在内存中，第一时间替换为黑色圆点符号。只有点击登录的时候才会回调真正的密码。
- 只是实现了功能，并没有做界面上的美化。

#### 使用说明

- 用起来也很简单，可以参考demo中TestController中的代码。路径：CustomedKeyboardDemo-master/CustomedKeyboardDemo/CustomedKeyboardDemo/DSKeyboard/Controllers

1.先导入头文件，#import "DSKyeboard.h" 

2.在视图加载完成后，对DSKyeboard进行初始化，并赋值给某个输入框的inputView属性。再通过接口- (void)dsKeyboardTextChangedOutputBlock:(DSKeyboardOutput)output loginBlock:(DSKeyboardLogin)login;设置回调的block即可。
```
- (void)setupCustomedKeyboard {
    self.tf.inputView = [DSKyeboard keyboardWithTextField:self.tf];
    
    __weak typeof(self) weakSelf = self;
    [(DSKyeboard *)self.tf.inputView dsKeyboardTextChangedOutputBlock:^(NSString *fakePassword) {
        //键盘有输入时回调
        __strong typeof(weakSelf) strongSelf = weakSelf;
        strongSelf.tf.text = fakePassword;
    } loginBlock:^(NSString *password) {
        //点击登录按钮时回调
        __strong typeof(weakSelf) strongSelf = weakSelf;
        strongSelf.passwrodLab.text = [NSString stringWithFormat:@"密码 : %@", password];
    }];
}
```

3.使用时只需要把views文件夹拖入自己的工程即可。路径：CustomedKeyboardDemo-master/CustomedKeyboardDemo/CustomedKeyboardDemo/DSKeyboard/Views

4.如果有任何疑问可以联系我，如果觉得对你有所帮助话给个Star✨吧！！🙂
