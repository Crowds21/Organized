
# Organized

- Organized 链滴帖子(暂时没有发)
- [从笔记管理到信息管理 · 语雀 (yuque.com)](https://www.yuque.com/siyuannote/ta09ls/ml7277)

## Panel
Panel 模板更新适配 1.2.5 版本.把查看昨天的Summary 通过SQL嵌入更改为了直接获取文本

## Catalogue
- Catalogue 生成当前文件夹下所有文档的目录(不包括子文档)
- Catalogue_Dyn 通过SQL嵌入生成文件夹下笔记块的目录(不包括子文档)
- Catalogue_Today 生成今天创建的笔记块的目录
- Catalogue_ALL 旧版的 Catalogue (不推荐在新版本思源中使用)

## Header使用说明
Header模板是我在对卡片盒笔记的个人实践,仅供参考
**Catalogue_Dyn 和 Catalogue_Today 都需要配合Header使用**
- @Aim 作用是充当标签
- 时间串作为一级标题我个人主要是为了方便折叠


为了让Header 获取最好的观赏效果,最好将下方的CSS 添加到你所用的主题中


### 配合Header 使用的 CSS
```css
/*HEADER部分*/
[data-node-id][custom-docinfo]{
	font-size: 15px!important; 
	padding:0px!important;
	font-style:italic;
	font-weight:bold;
}
[data-subtype=h1][data-node-id][custom-docinfo]{
	font-size: 18px!important; 
	padding:0px!important;
	font-style:italic!important;
}
```