# CardView的简单使用

标签（空格分隔）： Android_Material_Design CardView

---

##CardView简介##
CardView是Android5.0之后为新增的控件，CardView是一个卡片布局，布局可以包含圆角和阴影，本质上CardView是一个FrameLayout，因此它作为一个布局容器，可以布局其他的View。
##CardView属性##
CardView中常用的**属性**有：

 - `cardElevation`:设置阴影的大小
 - `cardBackgroundColor`:卡片布局的背景颜色
 - `cardCornerRadius`：卡片布局的圆角的大小
 - `conentPadding`：卡片布局和内容之间的距离
##示例代码CODE##
```Java
<?xml version="1.0" encoding="utf-8"?>
<android.support.v7.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginBottom="12dp"
    android:layout_marginTop="12dp"
    android:layout_marginLeft="15dp"
    android:layout_marginRight="15dp"
    app:cardBackgroundColor="@color/white"
    app:contentPadding="8dp"
    app:cardCornerRadius="10dp"
    app:cardElevation="10dp">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:paddingTop="8dp"
        android:paddingBottom="8dp"
        android:orientation="horizontal">
        <ImageView
            android:id="@+id/item_iv"
            android:layout_width="120dp"
            android:layout_height="90dp"
            android:layout_gravity="center_vertical"
            android:layout_margin="6dp"
            android:background="@drawable/item_one"
            android:scaleType="centerCrop"/>
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginLeft="6dp"
            android:layout_marginRight="10dp"
            android:layout_gravity="center_vertical"
            android:orientation="vertical">
            <TextView
                android:id="@+id/item_title_tv"
                android:layout_width="wrap_content"
                android:textColor="#383838"
                android:textSize="20sp"
                android:textStyle="bold"
                android:layout_height="wrap_content"
                android:text="非著名程序员"/>
            <TextView
                android:id="@+id/item_content_tv"
                android:textColor="#545454"
                android:textSize="16sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:text="美女说：非著名程序员公众号是东半球最好的技术分享公众号"/>
        </LinearLayout>
    </LinearLayout>
</android.support.v7.widget.CardView>
```
必须添加依赖	
   

     compile 'com.android.support:cardview-v7:23.4.0'
