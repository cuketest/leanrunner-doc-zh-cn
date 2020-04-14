## Windows应用自动化常见问题


<a id="datetimepicker"></a>
#### Q: DateTimePicker控件识别为Custom，应该如何操作？

**A**: DateTimePicker是一种组合控件，即由多个基本控件组成的，所以它的类型是Custom或是Pane(在Windows 10)下。下面是自动化组合控件的自动化样例，即如何获取它的值和设置它的值：

```javascript
    let datePicker = model.getCustom("dateTimePicker1")
    //获取DateTimePicker的值
    console.log('value=' + await datePicker.name())
    //设置DateTimePicker的值
    await datePicker.click(2, 2);
    await datePicker.pressKeys('2018-08-18')
```

获取值就是拿它的name属性，设置值就是点击前部，并pressKeys输入日期。

<a id="performance"></a>
#### Q: 如何提高自动化代码的运行效率

**A**: 可以尝试以下的实践，
1. 在目标控件是同一个时，可以将识别的控件对象赋值给变量，而不是每次都调用getXXX("controlName")获取对象。例如：
为了避免重复识别，可以写成：
   ```javascript
   let newControl = await model.getXXX('new control')
   await newControl.exists(10);
   await newControl.click() 
   ```
这样识别就只有一次。

2. 如果要操作的一组控件都在某一个容器控件下，可以先获取容器对象，然后调用容器对象获取该控件，也可以加快识别，因为减少了每次都从根对象识别的时间。
例如，"userName"编辑框、“password"编辑框和”login"按钮都在一个“Pane"容器控件下。可以写成下面的代码：

   ```javascript
   let pane = getPane('pane1`);
   let userName = await pane.getEdit('userName');
   //...operations on userName
   let password = await pane.getEdit('password');
   //...operations on password
   await pane.getButton('login').click();
   ```
   
>注意：并不是所有看起来都一样的控件都可以用缓存的{{book.test_object}}变量反复访问。例如，同一个菜单，分两次打开，则是不同的两个实例，如果第一次打开你缓存到变量中了，第二次点开这个菜单，你还想用刚才那个变量访问它就会出现无法识别的问题，因为这其实是两个控件实例。
建议避免用全局变量缓存对象，只应该用局部变量，如果在一次打开的界面中可以用变量缓存控件，并重复使用，如果控件是重新打开的，则不能重用它的{{book.test_object}}，而需要重新调model.getXXX方法获取一个新的对象。

<a id="promise"></a>
#### Q: 我的代码运行时出错，报UnhandledPromiseRejectionWarning: Unhandled promise rejection ...

**A**: 当执行的API函数是异步时，即它的返回值是Promise，并且调用时没有捕捉异常就会出这个错误信息。为获得具体的错误信息，可以在调用的代码中用try/catch语句包含抛错的代码，同时await这个Promise，这样异常就会被捕捉到，你可以在catch中处理这个错误，例如：

```javascript
(async function() {
   try {
      await model.getButton('button1').click();
   } catch(err) {
      console.log(err);
   }
}
```
如果button1对象不存在或识别不到，上述getButton会产生异常，并被捕捉并打印异常信息。





