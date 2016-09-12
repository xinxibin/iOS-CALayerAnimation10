# iOS-CALayerAnimation10

### 实现所需知识
* CAShapeLayer
* CAReplicatorLayer
* CAReplicatorLayer
* CAAnimationGroup

### 具体实现Code

```objc
//波纹，咻一咻，雷达效果

@property (nonatomic,strong)UIView *testView;


- (void)setup
{
    _testView=[[UIView alloc] initWithFrame:CGRectMake(30, 300, 100, 100)];
    _testView.center = self.view.center;
    [self.view addSubview:_testView];
    _testView.layer.backgroundColor = [UIColor clearColor].CGColor;
    
    CAShapeLayer *pulseLayer = [CAShapeLayer layer];
    pulseLayer.frame = _testView.layer.bounds;
    pulseLayer.path = [UIBezierPath bezierPathWithOvalInRect:pulseLayer.bounds].CGPath;
    pulseLayer.fillColor = [UIColor redColor].CGColor;//填充色
    pulseLayer.opacity = 0.0; // 层的透明度
    
    CAReplicatorLayer *replicatorLayer = [CAReplicatorLayer layer];
    replicatorLayer.frame = _testView.bounds;
    replicatorLayer.instanceCount = 8;//创建副本的数量,包括源对象。
    replicatorLayer.instanceDelay = 0.5;//复制副本之间的延迟
    [replicatorLayer addSublayer:pulseLayer];
    [_testView.layer addSublayer:replicatorLayer];
    
    CABasicAnimation *opacityAnima = [CABasicAnimation animationWithKeyPath:@"opacity"];
    opacityAnima.fromValue = @(0.3);
    opacityAnima.toValue = @(0.0);
    
    CABasicAnimation *scaleAnima = [CABasicAnimation animationWithKeyPath:@"transform"];
    scaleAnima.fromValue = [NSValue valueWithCATransform3D:CATransform3DScale(CATransform3DIdentity, 0.0, 0.0, 0.0)];
    scaleAnima.toValue = [NSValue valueWithCATransform3D:CATransform3DScale(CATransform3DIdentity, 2, 2, 0.0)];
    
    CAAnimationGroup *groupAnima = [CAAnimationGroup animation];
    groupAnima.animations = @[opacityAnima, scaleAnima];
    groupAnima.duration = 4.0;
    groupAnima.autoreverses = NO;
    groupAnima.repeatCount = HUGE;
    [pulseLayer addAnimation:groupAnima forKey:@"groupAnimation"];
    
    
}
```


![](http://oahmyhzk1.bkt.clouddn.com/image/gif/Corrugated%20animation.gif)

[扩展动画 点击 波纹效果](https://github.com/xinxibin/iOS-CALayerAnimation11)