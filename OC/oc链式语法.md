```objective-c


#define AAObject(objectName) [[objectName alloc]init]


#define AAPropStatementAndPropSetFuncStatement(propertyModifier,className, propertyPointerType, propertyName)           \
@property(nonatomic,propertyModifier)propertyPointerType  propertyName;                                                 \
- (className * (^) (propertyPointerType propertyName)) propertyName##Set;

#define AAPropSetFuncImplementation(className, propertyPointerType, propertyName)                                       \
- (className * (^) (propertyPointerType propertyName))propertyName##Set{                                                \
return ^(propertyPointerType propertyName) {                                                                            \
_##propertyName = propertyName;                                                                                         \
return self;                                                                                                            \
};                                                                                                                      \
}


使用示例:
.h文件中
@interface AATooltip : NSObject
//AAPropStatementAndPropSetFuncStatement(assign, AATooltip, BOOL,       animation) //是否启用动画是否启用动画(设置 animation == false,禁用 tooltip 动画能够在一定程度上节省程序的计算资源,提高运行效率,但是在现如今移动设备的性能如此强劲的时代大背景下,节省的这一点计算资源基本上没有任何意义,所以我注释掉了这个属性)
AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, backgroundColor) //背景色
AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, borderColor) //边框颜色
AAPropStatementAndPropSetFuncStatement(strong, AATooltip, NSNumber *, borderRadius) //边框的圆角半径
AAPropStatementAndPropSetFuncStatement(strong, AATooltip, NSNumber *, borderWidth) //边框宽度
AAPropStatementAndPropSetFuncStatement(strong, AATooltip, NSDictionary *, style) //为提示框添加CSS样式。提示框同样能够通过 CSS 类 .highcharts-tooltip 来设定样式。 默认是：@{@"color":@"#333333",@"cursor":@"default",@"fontSize":@"12px",@"pointerEvents":@"none",@"whiteSpace":@"nowrap" }

AAPropStatementAndPropSetFuncStatement(assign, AATooltip, BOOL,       enabled) 
AAPropStatementAndPropSetFuncStatement(assign, AATooltip, BOOL,       useHTML) 
AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, formatter) 
AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, headerFormat) 
AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, pointFormat) 
AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, footerFormat) 
AAPropStatementAndPropSetFuncStatement(strong, AATooltip, NSNumber *, valueDecimals) //设置取值精确到小数点后几位
AAPropStatementAndPropSetFuncStatement(assign, AATooltip, BOOL,       shared) 
AAPropStatementAndPropSetFuncStatement(assign, AATooltip, BOOL,       crosshairs) 

AAPropStatementAndPropSetFuncStatement(copy,   AATooltip, NSString *, valueSuffix) 
//AAPropStatementAndPropSetFuncStatement(assign, AATooltip, BOOL,       followTouchMove) //在触摸设备上，tooltip.followTouchMove选项为true（默认）时，平移需要两根手指。若要允许用一根手指平移，请将followTouchMove设置为false。
@end

.m文件中
@implementation AATooltip
//AAPropSetFuncImplementation(AATooltip, BOOL,       animation) //是否启用动画是否启用动画(设置 animation == false,禁用 tooltip 动画能够在一定程度上节省程序的计算资源,提高运行效率,但是在现如今移动设备的性能如此强劲的时代大背景下,节省的这一点计算资源基本上没有任何意义,所以我注释掉了这个属性)
AAPropSetFuncImplementation(AATooltip, NSString *, backgroundColor) //背景色
AAPropSetFuncImplementation(AATooltip, NSString *, borderColor) //边框颜色
AAPropSetFuncImplementation(AATooltip, NSNumber *, borderRadius) //边框的圆角半径
AAPropSetFuncImplementation(AATooltip, NSNumber *, borderWidth) //边框宽度
AAPropSetFuncImplementation(AATooltip, NSDictionary *, style) //为提示框添加CSS样式。提示框同样能够通过 CSS 类 .highcharts-tooltip 来设定样式。 默认是：@{@"color":@"#ffffff",@"cursor":@"default",@"fontSize":@"12px",@"pointerEvents":@"none",@"whiteSpace":@"nowrap" }

AAPropSetFuncImplementation(AATooltip, BOOL,       enabled) 
AAPropSetFuncImplementation(AATooltip, BOOL,       useHTML) 
AAPropSetFuncImplementation(AATooltip, NSString *, formatter) 
AAPropSetFuncImplementation(AATooltip, NSString *, headerFormat) 
AAPropSetFuncImplementation(AATooltip, NSString *, pointFormat) 
AAPropSetFuncImplementation(AATooltip, NSString *, footerFormat) 
AAPropSetFuncImplementation(AATooltip, NSNumber *, valueDecimals) //设置取值精确到小数点后几位
AAPropSetFuncImplementation(AATooltip, BOOL,       shared) 
AAPropSetFuncImplementation(AATooltip, BOOL,       crosshairs) 
AAPropSetFuncImplementation(AATooltip, NSString *, valueSuffix) 
//AAPropSetFuncImplementation(AATooltip, BOOL,       followTouchMove) 
@end

```

