.action{$docid:=.id}
.action{$docname:=.title}
.action{$block := (queryBlocks "select * from blocks where type='d' and id ='?' "  $docid)}
.action{$filePath :=" "}
.action{$fileBox :=" "}
.action{$dirPath := " "}
.action{$numOfSearch := 0}

.action{$regexDirPath:= "(/(\\w|-)*)+" }
.action{$today := now | date "20060102"}

.action{/*获取文件的目录路径*/}
	.action{range $index,$v:=$block}
		.action{$filePath = $v.Path}
		.action{$fileBox =  $v.Box}
	.action{end}
	
.action{/*通过正则表达式获取该文件所在的文件夹*/}
.action{$dirPath =(regexFind  $regexDirPath  $filePath )}
.action{/*获取目录包括子目录下所有的文件*/}
{{select * from blocks where path LIKE '.action{$dirPath}/.action{$today}______-_______.sy' and box='.action{$fileBox}' and content LIKE '@Aim:%'  order by created limit -1 }}
	



