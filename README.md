# Organized README


## 说明
- 模板的主要功能是日程管理,最好在同一个笔记本下使用
- 不需要修改模板和设置ID,主要通过 alias和name 属性实现互连.

## 组成
* Panel_Day
  * 日记模板
* Panel_Year
  * 将一年按照月显示,月则通过 周展示
* Panel_Week
  * 每周总览
  
* Info_Catalogue
  * 获取文件列表,包括自身
* Info_DocDscription
  * 简易的文件说明

##### TODO

* [ ] 模板的嵌套(代码可读性)
* [ ] WeekPanel 调整Days 和 Summary
  * [ ] 总结不去自己一点点写就没有意义.光是展示每天的总结不够
  * [ ] 总结部分需要一个单独的模板,能够统计这周编写的文件数目.然后将每天的总结 Content输出,而不是按照SQL的效果输出(太过于占据地方)
   * [ ] Days中的昨日总结,也可以输出 Content 我个人不喜欢太多的SQL块,看着很不舒服 或者是SQL查询结果去除掉标题
* [ ] 通用项目 说明以及项目资源统计 的文档
  
#### 2021年7月30日
- Panel_Week 周数生成调整 和排版的调整
- Panel_Day 增加昨日字数统计
- Panel_Day 增加最近三日编辑过的文本
- Panel_Day改进超级块会错误的继承内部块的属性
- 加入Info_Catalogue
- 调整 Panel_Week 的排版