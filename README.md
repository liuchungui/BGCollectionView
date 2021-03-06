# BGCollectionView
BGCollectionView是基于UICollectionView（纯代码方式）实现上下拉刷新加载数据的瀑布流式（WaterFlow）布局，
其中集成下拉刷新采用的是EGORefreshTableHeaderView。

##使用方法：

导入"WaterFlow"与"EGOTableViewPullRefresh"文件夹至目标工程中。

（1）创建自定义瀑布流式布局

```
BGCollectionViewFlowLayout *waterFlowLayout = [[BGCollectionViewFlowLayout alloc] init];
    waterFlowLayout.delegate = self;
    //设置列数
    waterFlowLayout.columnNum = 4;
    //设置间距
    waterFlowLayout.itemSpacing = 15;
    //设置组上下左右间距
    waterFlowLayout.bSectionInset = BGEdgeInsetsMake(10, 10, 10, 10);
```
    
（2）创建BGCollectionView

```
   BGCollectionView *waterFlowCollectionView = [[BGCollectionView alloc]initWithFrame:CGRectMake(0, 0, bScreenWidth, bScreenHeight - 64) collectionViewLayout:waterFlowLayout];
    waterFlowCollectionView.pullDownRefreshBlock = ^(UICollectionView *collectionView) {
        //下拉取最新数据
    };
    
    waterFlowCollectionView.pullUpRefreshBlock = ^(UICollectionView *collectionView) {
        //上拉取更多数据
    };
    [self.view addSubview:waterFlowCollectionView];
```
    
（3）实现BGCollectionViewFlowLayoutDelegate代理方法

```
- (CGFloat)collectionView:(UICollectionView *)collectionView
                   layout:(BGCollectionViewFlowLayout *)layout
 heightForItemAtIndexPath:(NSIndexPath *)indexPath
{
    //返回指定的高度
    return 100 + (rand() % 100);
}
```
