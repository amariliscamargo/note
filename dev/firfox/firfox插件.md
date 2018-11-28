# 火狐常用插件及配置

<!-- MarkdownTOC -->

- [Markdown Viewer Webext](#markdown-viewer-webext)

<!-- /MarkdownTOC -->
<a id="markdown-viewer-webext"></a>
### Markdown Viewer Webext
使浏览器支持 markdown 文件

如果乱码, 需要设置一些浏览器默认的编码方式为 utf8
在浏览器地址栏中输入: about:config
搜索 intl.charset.fallback.utf8_for_file 并将它的值改为 true

添加侧边栏的toc.将下面的 css 规则添加到插件中.
```css
.markdownRoot > h1 + ul {
  position: fixed;
  top: 0;
  left: 0;
  overflow: scroll;
  width: 18%;
  padding: 20px;
  height: 100vh;
  margin-top: 0;
  font-size: .75rem;
}
.markdownRoot {
  width: 80%;
  margin-left: 20%;
  min-height: 200vh;
  padding: 0 1em;
}
```
