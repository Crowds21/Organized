.action{$docid:=.id}
.action{$docname:=.title}
.action{$block := (queryBlocks "select * from blocks where type='d' and id ='?' "  $docid)}
.action{$filePath :=" "}
.action{$fileBox :=" "}
.action{$dirPath := " "}
.action{$numOfSearch := 0}

.action{$regexDirPath:= "(/(|\\w|-)*)+" }


.action{/*获取文件的目录路径*/}
	.action{range $index,$v:=$block}
		.action{$filePath = $v.Path}
		.action{$fileBox =  $v.Box}
	.action{end}
.action{/*通过正则表达式获取该文件所在的文件夹*/}
.action{$dirPath =(regexFind  $regexDirPath  $filePath )}
.action{/*获取目录包括子目录下所有的文件*/}
.action{$block := (queryBlocks "select * from blocks where path LIKE '?/______________-_______.sy' and type='d' and box='?' order by path limit -1"  $dirPath $fileBox)}
	

.action{/*输出当前文件夹下的文档(不包括子文档)*/}
.action{range $index, $v:=$block}
- ((.action{$v.ID}))
.action{end}

