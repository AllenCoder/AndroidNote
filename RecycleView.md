

#设置 item  click 
Adapter
```java
mRecyclerView.addOnItemTouchListener(new OnItemClickListener(mRecyclerView,mQuickAdapter){

            @Override
            public void SimpleOnItemClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();
                
            }
        });
        
```
#设置 it item child click
首先需要添加需要点击触发的 childview id 
``` 
 @Override
    protected void convert(BaseViewHolder helper, Status item) {
        helper.setText(R.id.tweetName, item.getUserName())
                .setText(R.id.tweetText, item.getText())
                .setText(R.id.tweetDate, item.getCreatedAt())
                .setVisible(R.id.tweetRT, item.isRetweet())
                .addOnClickListener(R.id.tweetAvatar)
                .addOnClickListener(R.id.tweetName)
                .addOnLongClickListener(R.id.tweetText)
                .linkify(R.id.tweetText);
        Glide.with(mContext).load(item.getUserAvatar()).crossFade().placeholder(R.mipmap.def_head).transform(new GlideCircleTransform(mContext)).into((ImageView) helper.getView(R.id.tweetAvatar));
    }
```
然后
```java
   mRecyclerView.addOnItemTouchListener(new OnItemChildClickListener(mRecyclerView,mQuickAdapter) {
            @Override
            public void SimpleOnItemChildClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();

            }
        });
```
#设置 it item long click
```java
 mRecyclerView.addOnItemTouchListener(new OnItemLongClickListener(mRecyclerView,mQuickAdapter) {
            @Override
            public void SimpleOnItemLongClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();

            }
        });
```
#设置 it item child long click
首先需要添加需要点击触发的 childview id 
``` 
 @Override
    protected void convert(BaseViewHolder helper, Status item) {
        helper.setText(R.id.tweetName, item.getUserName())
                .setText(R.id.tweetText, item.getText())
                .setText(R.id.tweetDate, item.getCreatedAt())
                .setVisible(R.id.tweetRT, item.isRetweet())
                .addOnClickListener(R.id.tweetAvatar)
                .addOnClickListener(R.id.tweetName)
                .addOnLongClickListener(R.id.tweetText)
                .linkify(R.id.tweetText);
        Glide.with(mContext).load(item.getUserAvatar()).crossFade().placeholder(R.mipmap.def_head).transform(new GlideCircleTransform(mContext)).into((ImageView) helper.getView(R.id.tweetAvatar));
    }
```
然后
```java
 mRecyclerView.addOnItemTouchListener(new OnItemChildLongClickListener(mRecyclerView,mQuickAdapter) {
            @Override
            public void SimpleOnItemChildLongClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();
            }
        });
```
# 如果你想实现多种点击事件，你可以实现 SimpleClickListener类。提供了丰富的事件点击封装
```java
 mRecyclerView.addOnItemTouchListener(new SimpleClickListener(mRecyclerView, mQuickAdapter) {
            @Override
            public void onItemClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onItemLongClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onItemChildClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onItemChildLongClick(BaseQuickAdapter adapter, View view, int position) {
                Toast.makeText(RecyclerClickItemActivity.this, "" + Integer.toString(position), Toast.LENGTH_SHORT).show();
            }
        });
``` 
