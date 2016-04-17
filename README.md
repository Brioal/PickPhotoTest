#调用系统相册获取图片并显示
##本方法获取到的图片相当于只是一张缩略图，本来应该包含直接返回图片的绝对路径的，但网上的方法大多都是不能用的，再琢磨一阵后会补全这个坑
##效果图：
![这里写图片描述](http://img.blog.csdn.net/20160417131644331)
##步骤：

 1. 以`startActivityForResult`的方法调用系统图库
 2. 选择图片
 3. `onActivityResult`方法获取返回的内容，显示到屏幕上


##实现方法：
###1.调用系统图库：
```
Intent intent = new Intent(Intent.ACTION_PICK);
        intent.setType("image/*"); //照片类型
        startActivityForResult(intent, 0);
```
###2.选择图片：略
###3.获取返回的数据并显示
```
//重写onAcrtivityResult方法来实现
@Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (resultCode == RESULT_OK && requestCode == 0) {
            Uri uri = data.getData();
            Bitmap bitmap = null;
            try {
                bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), uri);
               //...图片操作
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```


##在上一个Demo中使用过，故记录一下，上一篇地址：
 [二维码扫描库的使用](http://blog.csdn.net/qq_26971803/article/details/51171203)
