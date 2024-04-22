## 链接

[SVG ICON 生成](https://fffuel.co/)

> 如何处理图标文件 favicon.ico
## 准备 SVG 文件

[Favicons 媒体查询技术](https://evilmartians.com/chronicles/how-to-use-p3-colors-in-svg)

```svg
 <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
 </svg>
```
## 创建 ICO 文件

[Inkscape](https://inkscape.org/)
[ImageMagick](https://www.imagemagick.org/script/download.php)

```sh
# 生成 png
inkscape ./icon.svg --export-width=32 --export-filename="./tmp.png"
# 生成 ico
(imageMagick) convert ./tmp.png ./favicon.ico
```
## 创建不同大小 PNG

```sh
inkscape --export-type="png" --export-width=512 --export-filename="./icon-512.png" ./icon.svg
```
## 优化 PNG SVG 文件

[SVGO](https://github.com/svg/svgo)
[Squoosh](https://squoosh.app/)

```sh
npx svgo --mutlipass icon.svg
```