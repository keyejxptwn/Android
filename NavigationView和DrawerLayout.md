# NavigationView和DrawerLayout实现侧滑菜单栏(抽屉)

标签（空格分隔）： android view

---

##1.  DrawerLayout
:    可以实现左滑和右滑功能，只要在layout文件中配置好左右两个抽屉就可以了，左右两个抽屉可以是任意的view，结合NavigationView可以很好实现侧滑菜单的功能,要使用***DrawerLayout***,需要***v4***包，使用***NavigationView***，需要***design***包
```java
 compile 'com.android.support:design:23.2.1'
```
---
>  效果:
-  ![效果图][1]
  [1]: http://www.it165.net/uploadfile/files/2015/0712/20150712160557727.gif
布局文件：
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.qianfeng.zhouyi.drawerlayouttest.MainActivity">

   <FrameLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"/>

    <android.support.design.widget.NavigationView
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="left"
        app:headerLayout="@layout/layout_navhead"
        app:menu="@menu/mymenu"
        android:id="@+id/navTest"
        
        />


</android.support.v4.widget.DrawerLayout>
```
- [x] drawlayout只需要配置***layout_gravity***属性为“**left**”或“**right**”即可自动构建左边或右边的抽屉，也可两个都配置
> headerLayout就是给导航栏增加一个头部Layout。
  menu就是对应菜单项的选择条目。

```xml
navigation_header.xml

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="200dp"
    android:background="#30469b">

<TextView
    android:id="@+id/header_tv"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_centerInParent="true"
    android:text="HeaderLayout"
    android:textColor="#ffffff"
    android:textSize="25sp" />
    
</RelativeLayout>
```
```xml
drawer.xml

<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
<group android:checkableBehavior="single">
<item
    android:id="@+id/item_one"
    android:icon="@mipmap/icon"
    android:title="我的动态"></item>
<item
    android:id="@+id/item_two"
    android:icon="@mipmap/icon"
    android:title="我的留言"></item>
<item
    android:id="@+id/item_three"
    android:icon="@mipmap/icon"
    android:title="附近的人"></item>
</group>
</menu>

```
- [x] 设置navigationview的菜单响应
```java
//设置导航栏NavigationView的点击事件
NavigationView mNavigationView = (NavigationView) findViewById(R.id.navigation_view);
mNavigationView.setNavigationItemSelectedListener(new NavigationView.OnNavigationItemSelectedListener() {
    @Override
    public boolean onNavigationItemSelected(MenuItem menuItem) {
        switch (menuItem.getItemId()) {
            case R.id.item_one:
                getSupportFragmentManager().beginTransaction().replace(R.id.frame_content, new FragmentOne()).commit();
                mToolbar.setTitle("我的动态");
                break;
            case R.id.item_two:
                getSupportFragmentManager().beginTransaction().replace(R.id.frame_content, new FragmentTwo()).commit();
                mToolbar.setTitle("我的留言");
                break;
            case R.id.item_three:
                getSupportFragmentManager().beginTransaction().replace(R.id.frame_content, new FragmentThree()).commit();
                mToolbar.setTitle("附近的人");
                break;
        }
        menuItem.setChecked(true);//点击了把它设为选中状态
        mDrawerLayout.closeDrawers();//关闭抽屉
        return true;
    }
});
```
- [ ] 练习：把navigationview用listview替代
```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/drawerlayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <!--定义内容区的布局-->
    <FrameLayout
        android:id="@+id/content"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

    <!-- &lt;!&ndash;定义右抽屉的布局&ndash;&gt;
     <android.support.design.widget.NavigationView
         android:id="@+id/navleft"
         android:layout_width="match_parent"
         android:layout_height="match_parent"
         app:headerLayout="@layout/layout_navheader"
         app:menu="@menu/mune_nav"
         android:layout_gravity="left" />-->
    <ListView
        android:background="#ffffff"
        android:id="@+id/listview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_gravity="left"
        />

</android.support.v4.widget.DrawerLayout>
```
-  MainActivty.java
```java
package com.qf.smile.navigationdemo;

import android.os.Bundle;
import android.support.v4.widget.DrawerLayout;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;

import com.lidroid.xutils.ViewUtils;
import com.lidroid.xutils.view.annotation.ViewInject;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {
    /*@ViewInject(R.id.navleft)
    private NavigationView leftNavView;*/
    @ViewInject(R.id.listview)
    private ListView listView;
    @ViewInject(R.id.drawerlayout)
    private DrawerLayout drawerlayout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_nav);

        ViewUtils.inject(this);
        List<String> datas = new ArrayList<>();
        for (int i = 0; i < 5; i++) {
            datas.add("" + (i + 1));
        }
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, datas);
        listView.addHeaderView(getLayoutInflater().inflate(R.layout.layout_navheader, listView, false));
        listView.setAdapter(adapter);
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                drawerlayout.closeDrawers();
            }
        });
        /*leftNavView.setNavigationItemSelectedListener(new NavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(MenuItem item) {
                int id = item.getItemId();
                switch (id) {
                    case R.id.item1:
                        Toast.makeText(MainActivity.this,"我的动态被点击了",Toast.LENGTH_SHORT).show();
                        getSupportFragmentManager().beginTransaction().replace(R.id.content,new DynamicFragment()).commit();
                        break;
                    case R.id.item2:
                        Toast.makeText(MainActivity.this,"我的留言被点击了",Toast.LENGTH_SHORT).show();
                        getSupportFragmentManager().beginTransaction().replace(R.id.content,new GuestbookFragment()).commit();
                        break;
                    case R.id.item3:
                        Toast.makeText(MainActivity.this,"附近的人被点击了",Toast.LENGTH_SHORT).show();
                        getSupportFragmentManager().beginTransaction().replace(R.id.content,new NearPersonFragment()).commit();
                        break;
                    case R.id.item4:
                        MainActivity.this.finish();
                        break;
                    default:
                        break;
                }
                item.setChecked(true);//把当前点选的菜单先设置为选中的样式
                drawerlayout.closeDrawers();//关闭
                return false;
            }
        });*/
    }
}

```
