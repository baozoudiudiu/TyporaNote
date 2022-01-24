给UITableViewHeaderFooterView设置背景色分2种情况

1.tableView在group模式下，UITableViewHeaderFooterView的背景色默认是透明的，此时如果要设置背景色只需要给contentView设置颜色即可

```
self.contentView.backgroundColor = [UIColor redColor];
```



2.tableView在plain模式下，这个时候UITableViewHeaderFooterView默认有个浅灰色背景，如果要让背景色为clearColor,就不能直接设置self 和 self.contentView的颜色，经过测试发现，这样设置是不会生效的，正确的方式可以通过下面方法来实现

```
-(void)tableView:(UITableView *)tableView willDisplayHeaderView:(UIView *)view forSection:(NSInteger)section {

  if ([view isMemberOfClass:[UITableViewHeaderFooterView class]]) {

​    ((UITableViewHeaderFooterView *)view).backgroundView.backgroundColor = [UIColor clearColor];

  }

}
```



注意isMemberOfClass和isKindOfClass的区别，目的是到这里找到你需要的UITableViewHeaderFooterView并设置背景色为透明