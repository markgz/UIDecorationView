# UIDecorationView
https://markpospesel.wordpress.com/2012/12/11/decorationviews/

# IOS: CHANGING THE SECTION BACKGROUND COLOR IN A UICOLLECTIONVIEW
http://www.ericjchapman.com/ios-changing-the-section-background-color-in-a-uicollectionview.html

# setup SSH bitbucket
https://confluence.atlassian.com/bitbucket/troubleshoot-ssh-issues-271943403.html

# 更新宿主项目对应的子模块
git submodule update --init --recursive


## 2015年10月28日工作日记
1.完成基本的UICollection布局，使用到UICollectionView的 Decoration View。需要重写UICollectionFlowLayout 和 UICollectionViewLayoutAttributes。还需要继续和真实数据对接。

CoreData第一次加载的时候，为什么是空，第二次启动应用就正常了。

## 2015年10月29日工作笔记

问题二已经解决，因为使用到三个NSManagedObjectContext，一个tempContext，一个mainContext，一个backgroundContext，它们的关系是tempContext的parentContext是mainContext，mainContext的parentContext是backgroundContext。backgroundContext才关联持久化协调器。也就是要backgroundContext调用了save方法没有出错后，才表示已经存储到磁盘上了。这个问题的原因也就是在backgroundContext的save方法完成前，使用NSFetchredResutlController去执行performFetch。但是performFetch后的fetchResult居然不为空，但是对应的sectionInfo却是空的（因为在创建NSFetchedResultsController的时候，没有指定cacheName。导致sectionInfo是没有缓存的）。建议在backgroundContext的save方法后再去performFetch，如果成功performFetch后，记得reloadData。


问题一，有一种方法是对每一个section设置对应的Decoration View。在Github上有个链接是介绍如何实现这样的需求。

代码规范约定1：在viewController里的私有方法使用下划线开头_XXX

新问题1. 不能设置UICollectionViewCell的阴影效果。还没有找到具体的原因。
