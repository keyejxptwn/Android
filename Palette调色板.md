标签（空格分隔）： Android_Material_Design Palette
#Palette(调色板)
##Palette介绍##
Palette顾名思义**调色板**， Palette的作用是可以从**图像中提取图片的颜色**。我们可以把提取的颜色融入到App UI中，可以使UI风格更加美观融洽。
Palette可以提取的颜色如下：
```Java
Vibrant （有活力的）
Vibrant dark（有活力的 暗色）
Vibrant light（有活力的 亮色）
Muted （柔和的）
Muted dark（柔和的 暗色）
Muted light（柔和的 亮色）
```


----------
通过Palette对象获取到六个样本swatch
```Java
Palette.Swatch s = p.getVibrantSwatch();       //获取到充满活力的这种色调
Palette.Swatch s = p.getDarkVibrantSwatch();    //获取充满活力的黑
Palette.Swatch s = p.getLightVibrantSwatch();   //获取充满活力的亮
Palette.Swatch s = p.getMutedSwatch();           //获取柔和的色调
Palette.Swatch s = p.getDarkMutedSwatch();      //获取柔和的黑
Palette.Swatch s = p.getLightMutedSwatch();    //获取柔和的亮
```
swatch对象对应的颜色方法
```Java
getPopulation():            //像素的数量
getRgb():                   //RGB颜色
getHsl():                   //HSL颜色
getBodyTextColor():         //用于内容文本的颜色
getTitleTextColor():        //标题文本的颜色
```
##使用步骤##

 - 添加依赖
```Java
compile 'com.android.support:palette-v7:23.4.0'
```
  - 创建Palette对象，并获取图片的颜色值
```Java
// 用来提取颜色的Bitmap
Bitmap bitmap = BitmapFactory.decodeResource(getResources(), PaletteFragment.getBackgroundBitmapPosition(position));
// Palette的部分
Palette.Builder builder = Palette.from(bitmap);
builder.generate(new Palette.PaletteAsyncListener() {@Override public void onGenerated(Palette palette) {
        //获取到充满活力的这种色调
        Palette.Swatch vibrant = palette.getVibrantSwatch();
        //根据调色板Palette获取到图片中的颜色设置到toolbar和tab中背景，标题等，使整个UI界面颜色统一
        toolbar_tab.setBackgroundColor(vibrant.getRgb());
        toolbar_tab.setSelectedTabIndicatorColor(colorBurn(vibrant.getRgb()));
        toolbar.setBackgroundColor(vibrant.getRgb());
        if (android.os.Build.VERSION.SDK_INT >= 21) {
            Window window = getWindow();
            window.setStatusBarColor(colorBurn(vibrant.getRgb()));
            window.setNavigationBarColor(colorBurn(vibrant.getRgb()));
        }
    }
});
```
