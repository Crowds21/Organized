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
	.action{$docPath = $v.Path}
	.action{$docCreated = toDate "20060102150405" $v.Created | date "2006-01-02"}
	.action{$docUpdated = $v.Updated}	
.action{end}

.action{/*获取今天的开始时间*/}
.action{$today:=now|date "20060102"}
.action{$today = cat $today "000000"}
.action{$today = nospace $today}
.action{/*定义变量*/}
.action{$firstBlock := " "}
.action{$thisBlock := " "}
.action{$lastBlock := " "}
.action{$duration:= 0.0}
.action{$workHours:= 0.0}
.action{$flag := 0}

.action{/*获取中断时间和总时长*/}
{{{row
.action{$recent_block := (queryBlocks "SELECT * FROM blocks WHERE root_id = '?'  and updated >'?' order by updated limit -1 " $docID $today)}
.action{range $index,$v:=$recent_block}
	.action{$thisBlock = $v.Updated}
	.action{/*获取今天第一个创建的块*/}
	.action{if eq $index 0}
		.action{$firstBlock = $v.Updated }
		.action{$lastBlock = $firstBlock}
	.action{else}
		.action{$duration:= ((toDate "20060102150405" $thisBlock).Sub  (toDate "20060102150405" $lastBlock)).Minutes }
		.action{if gt $duration 15.0 }
		.action{$flag = 1}
@Interrupted .action{toDate "20060102150405" $firstBlock | date "15:04"} - .action{toDate "20060102150405" $lastBlock | date "15:04"}
			.action{$workHours = addf $workHours ((toDate "20060102150405" $lastBlock).Sub  (toDate "20060102150405" $firstBlock)).Minutes }
			.action{$firstBlock = $thisBlock}
		.action{end}
	.action{end}
	.action{$lastBlock = $thisBlock}
.action{end}

.action{/*如果中途有被打断,输出最后一段时间*/}
.action{if eq $flag 1}
	@Interrupted .action{toDate "20060102150405" $firstBlock | date "15:04"} - .action{toDate "20060102150405" $lastBlock | date "15:04"}
.action{end}
.action{$workHours = addf $workHours ((toDate "20060102150405" $lastBlock).Sub  (toDate "20060102150405" $firstBlock)).Minutes }

.action{$workHours = (divf ($workHours|int64) 60)| toString }
.action{$workHours = regexFind "\\w*\\.\\w\\w" $workHours}
@Duration .action{now|date "2006-01-02 15:04:05"} | .action{$workHours} h
}}}
{: name="@DocInfo" alias="@Duration" }
