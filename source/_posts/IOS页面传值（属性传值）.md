---
title: IOS页面传值（属性传值）
date: 2018-07-01 16:03:52
tags: IOS
---





![放张美图放放松](https://images.pexels.com/photos/733174/pexels-photo-733174.jpeg?cs=srgb&dl=adventure-asia-background-733174.jpg&fm=jpg)



##### (一)属性传值

我们先理下应用场景，例：页面1向页面2传值

1. 那我们需要在页面2 声明一个属性 看代码

```
//
//  NextViewController.h
//  ios_form
//  页面2
//  Created by Wenshuo on 2018/6/30.
//  Copyright © 2018年 Wenshuo. All rights reserved.
//
#import <UIKit/UIKit.h>
@interface NextViewController : UIViewController
//声明的属性
@property(strong,nonatomic) NSString *strValue;
@end
```



1. 页面1发送数据

```
//
//  ViewController.m
//  ios_form
//  页面1
//  Created by Wenshuo on 2018/6/30.
//  Copyright © 2018年 Wenshuo. All rights reserved.
//

#import "ViewController.h"
#import "NextViewController.h"
@interface ViewController ()
@property (nonatomic,strong) UILabel *label;
@property (nonatomic,strong) UIButton *btn;
@end

@implementation ViewController
-(UILabel *)label{
    if (_label==nil) {
        _label=[[UILabel alloc]initWithFrame:CGRectMake(100, 100, 200, 40)];
        _label.backgroundColor=[UIColor blackColor];
        _label.textColor=[UIColor whiteColor];
        _label.font=[UIFont systemFontOfSize:20];
    }
    return _label;
}

-(UIButton *)btn{
    if (_btn==nil) {
        _btn=[[UIButton alloc]initWithFrame:CGRectMake(100, 200, 200, 40)];
        _btn.backgroundColor=[UIColor redColor];
        [_btn setTitle:@"跳转至页面2" forState:UIControlStateNormal];
        [_btn setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];
       //添加按钮的点击事件btnClick
       [_btn addTarget:self action:@selector(btnClick) forControlEvents:UIControlEventTouchUpInside];
    }
    return _btn;
}

-(void)btnClick{
    NextViewController *nextVC=[[NextViewController alloc]init];
    //在这里对页面的声明的属性赋值
    nextVC.strValue=@"这是一个伤心的故事";
    //启动跳转
    [self presentViewController:nextVC animated:YES completion:nil];
}
//手动添加view  
- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
    [self.view addSubview:self.label];
    [self.view addSubview:self.btn];
}


- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end
```



1. 然后页面2接收

```
#import "NextViewController.h"

@interface NextViewController ()

@property (nonatomic,strong) UITextField *textfiled;
@property (strong,nonatomic) UIButton *btn;
@end

@implementation NextViewController
//懒加载的方式加载控件
-(UIButton *)btn{
    if (!_btn) {
        _btn=[[UIButton alloc]initWithFrame:CGRectMake(100,100,200,40)];
        _btn.backgroundColor=[UIColor redColor];
        [_btn setTitle:@"跳转回页面1" forState:UIControlStateNormal];
        [_btn setTitleColor:[UIColor whiteColor] forState:UIControlStateNormal];
        _btn.titleLabel.font =[UIFont systemFontOfSize:20];
        [_btn addTarget:self action:@selector(btnClick) forControlEvents:UIControlEventTouchUpInside];
    }
    return _btn;
}

-(UITextField *)textfiled{
    if(!_textfiled){
        _textfiled=[[UITextField alloc]initWithFrame:CGRectMake(100,300,200,40)];
        _textfiled.borderStyle=UITextBorderStyleLine;//设置边框
        _textfiled.text=self.strValue;//读取页面1的传值
    }
    return _textfiled;
}

-(void)btnClick{
    [self dismissViewControllerAnimated:YES completion:nil];
}

- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor=[UIColor whiteColor];
    // Do any additional setup after loading the view.
    //添加控件
    [self.view addSubview:self.textfiled];
    [self.view addSubview:self.btn];
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

/*
#pragma mark - Navigation

// In a storyboard-based application, you will often want to do a little preparation before navigation
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
    // Get the new view controller using [segue destinationViewController].
    // Pass the selected object to the new view controller.
}
*/

@end

```

这个传值方式非常容易理解！ 用java来看就是对对象的属性赋值