# hht_updateBootanim
`hht_updateBootanim.sh`是从学校HiteVision黑板Android系统中导出的开机动画更新脚本，其中记录有使用U盘更新系统开机动画的方法。

`usbdisk/`为U盘根目录示例，`bootanims/`有一些横屏适用的开机动画**注意，这些文件适用于直接替换`/system/media/bootanimation.zip`来更新开机动画，U盘更新方法最多支持part0、part1两个阶段。**

## 更新方法

1. U盘中`update_bootanimation`目录为标记,插入U盘时检测有此目录则尝试更新logo/bootanimation

2. 标记目录中可以全是图片(jpg/png),如果有`logo.jpg`文件则将此文件作为logo进行替换,其余作为`bootanimation/part0/`中内容来更新bootanimation

3. 标记目录中如果同时有part0/part1两个目录,则认为需要将这两个目录作为bootanimation的两个阶段内容来更新bootanimation,此时不考虑标记目录下图片

4. 标记目录中如果有`desc.txt`文件,则用此文件,不生成`desc.txt`.

5. 默认生成的`desc.txt`中指定图片分辨率为1920x1080,播放频率30.如果只有part0则无间隔无限重复,如果有part0/part1则part0无间隔播放1次part1无间隔无限播放.如果用此默认参数效果不佳,则提供`desc.txt`

6. 更新logo在`/tvconfig/boot0.jpg`,更新bootanimation在`/data/system/bootanimation.zip`

7. logo/bootanimation两者之一有更新则自动重启,重启后能看到更新后的效果

8. 更新过后U盘可能仍然插在大屏上,再次触发升级时会比对新旧logo的MD5,如果相同则不再更新logo;比对bootanimation中图片的MD5,如果标记目录中有`desc.txt`也比对此文件,如果相同则不更新bootanimation

9. logo和bootanimation可以单独更新,`desc.txt`不可单独更新需要有图片文件作为前提
