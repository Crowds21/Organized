.action{/*获取文档的基本信息*/}
.action{$docID:=.id}
.action{$docTitle := .title}
.action{$docBox :=" "}
.action{$docPath := " "}
.action{$docCreated := " "}
.action{$docUpdated := " "}
.action{$getDocInfo := (queryBlocks "SELECT * FROM blocks WHERE id='?' and type='d' " $docID )}
.action{range $v:= $getDocInfo}
	.action{$docBox =$v.Box}
	.action{$docPath = $v.HPath}
	.action{$docCreated = toDate "20060102150405" $v.Created | date "2006-01-02"}
	.action{$docUpdated = $v.Updated}	
.action{end}

{: name=""}

{: name=""}
.action{/*DOCPART*/}
--- 
# .action{now | date "2006/01/02 15:04:05"}
{: custom-docinfo="@sign"}
@Aim: .
{: custom-docinfo="@aim"}
@Point: .
{: custom-docinfo="@point"}

---
###### 正文

