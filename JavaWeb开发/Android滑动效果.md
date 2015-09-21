##Android 左右滑动

* ViewPager

	根据继承关系我们可以看出，ViewPager不在android sdk 自带jar包中，来源google 的补充组件android-support-v4.jar中，所以我们在3.0以前的版本中使用就需要导入该jar包了。

* ViewFlipper

	ViewFilpper控件是系统自带控件之一，主要用于在同一个屏幕间的切换及设置动画效果、间隔时间，且可以自动播放。
*  ViewFlow
	
	ViewFlow不是google官方的api，它是gethub上的一个开源项目，利用ViewFlow可以产生视图切换的效果。ViewFlow 相当于 Android UI 部件提供水平滚动的 ViewGroup，使用 Adapter 进行条目绑定，例如ViewPager或是ViewFlipper。它提供了三个组件ViewFlow、FlowIndicator和TitleFlowIndicator,一般情况下，当你需要做一个滑动然而不确定view的数目时，可以考虑使用ViewFlow。如果你的view数目确定，使用Fragments 或兼容库里的ViewPager比较好 。