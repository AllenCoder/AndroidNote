# Android ListView/RecyclerView notifyDatasetChanged刷新你真的熟悉吗？

1. ```
    /**
     * Returns whether RecyclerView is currently computing a layout.
     * <p>
     * If this method returns true, it means that RecyclerView is in a lockdown state and any
     * attempt to update adapter contents will result in an exception because adapter contents
     * cannot be changed while RecyclerView is trying to compute the layout.
     * <p>
     * It is very unlikely that your code will be running during this state as it is
     * called by the framework when a layout traversal happens or RecyclerView starts to scroll
     * in response to system events (touch, accessibility etc).
     * <p>
     * This case may happen if you have some custom logic to change adapter contents in
     * response to a View callback (e.g. focus change callback) which might be triggered during a
     * layout calculation. In these cases, you should just postpone the change using a Handler or a
     * similar mechanism.
     *
     * @return <code>true</code> if RecyclerView is currently computing a layout, <code>false</code>
     *         otherwise
     */
    public boolean isComputingLayout() {
        return mLayoutOrScrollCounter > 0;
    }
    ```

    
    
    ``` 
     返回是否RecyclerView当前计算的布局。
     *<P>
     *如果这个方法返回true，则意味着RecyclerView处于锁定状态，任何
     *试图更新适配器内容将导致一个异常，因为适配器内容
     而RecyclerView试图计算布局*不能改变。
     *<P>
     *这是不太可能，你的代码将在此状态下运行，因为它是
     *框架调用时布局遍历发生或RecyclerView开始滚动
     *响应于系统事件（触摸，辅助等）。
     *<P>
     *如果你有一些自定义逻辑来更改适配器内容，在这种情况下可能发生
     *响应查看回调（例如焦点更改回调），这可能会在一个被触发
     *布局计算。在这种情况下，你应该使用处理程序或只是推迟变化
     *类似的机制。
    ```
