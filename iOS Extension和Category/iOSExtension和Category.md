# iOS Extension 和 Category

## Category

Categroy 创建以后会有.h 和 .m文件 , 作用主要是为了实现主类的拓展，可以新增方法，但是不可新增属性

举例说明 原类是 HomeViewController，创建完成分类以后，出现HomeViewController+Categray.h  HomeViewController+Categray.m 两个文件

.h文件代码如下

#import "HomeViewController.h"

@interface HomeViewController (Categray)
-(void)sayHello;
@end


.m代码如下

#import "HomeViewController+Categray.h"

@implementation HomeViewController (Categray)

-(void)sayHello{
    NSLog(@"Hello");
}
@end

声明和实现都在分类中。


## Extension
Extension创建之后只有一个头文件，HomeViewController+Extension.h 

HomeViewController+Extension.h 代码如下：

#import "HomeViewController.h"

@interface HomeViewController ()
@property(nonatomic,copy)NSString *name;
-(void)sayHello();

@end


方法的实现和属性使用都在原来的HomeViewController.m 中

@implementation HomeViewController

-(void)sayHello{
    NSLog(@"%@",self.name);
}


## Category和Extension的区别

我们可以推导出一个明显的事实，extension可以添加实例变量，而category是无法添加实例变量的（因为在运行期，对象的内存布局已经确定，如果添加实例变量就会破坏类的内部布局，这对编译型语言来说是灾难性的）。

extension在编译期决议，它就是类的一部分，但是category则完全不一样，它是在运行期决议的。extension在编译期和头文件里的@interface以及实现文件里的@implement一起形成一个完整的类，它、extension伴随类的产生而产生，亦随之一起消亡。
extension一般用来隐藏类的私有信息，你必须有一个类的源码才能为一个类添加extension，所以你无法为系统的类比如NSString添加extension，除非创建子类再添加extension。而category不需要有类的源码，我们可以给系统提供的类添加category。
extension可以添加实例变量，而category不可以。
extension和category都可以添加属性，但是category的属性不能生成成员变量和getter、setter方法的实现。
