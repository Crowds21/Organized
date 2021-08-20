.action{/*获取文档的基本信息*/}
.action{$notebox :=" "}
.action{$docid:=.id}
.action{$getdocInfo := (queryBlocks "SELECT * FROM blocks WHERE id='?' and type='d' " $docid )}
.action{range $v:= $getdocInfo}
	.action{$notebox =$v.Box}	
.action{end}

.action{/*获取当前是第几周*/}
	.action{$ng_duration := (toDate "2006-01-02" "2020-12-28").Sub now}
	.action{$weekhours:=mul 7 24}
	.action{$duration:=sub 0 $ng_duration.Hours }
	.action{$week := div $duration $weekhours}
	.action{$today:= (now | date "2006-01")}
	.action{$weekResult:= (list $today "Week" $week| join " ")}


# .action{now | date "2006-01-02"}Diary
{: alias=".action{$weekResult}"}
.action{/*大致估算编辑的字数*/}
	.action{$yesterday := now | date_modify "-24h" | date "20060102150405"}
	.action{$words:=0}
	.action{$words_block := (queryBlocks "SELECT * FROM blocks WHERE ( updated >'?' or created >'?') order by path limit -1" $notebox $yesterday  $yesterday  )}
	.action{range $v:= $words_block}
		.action{$words =add $words (len $v.Content) }
	.action{end}
> 昨天你一共编辑了 **.action{$words}** 字


## Summary-Yesterday
.action{$yesterday:=(now | date_modify "-24h") | date "2006-01-02"}
.action{$summary_blocks := (queryBlocks "select * from blocks where box like '?' and hpath like '%?%' and parent_id in ( select id from blocks  where box like '?'  and type='h' and content = 'Summary' and hpath like '%?%') order by created" $notebox $yesterday $notebox $yesterday )}
	
.action{range $v:= $summary_blocks}
.action{$v.Markdown}
.action{end}


{{{col
{{{ 
## Schedule
{: name=".action{now | date "2006-01-02"}"}
- [ ] Task1
- [ ] Task2


## Summary
{: alias=".action{now | date "2006-01"} Week .action{$week}" name=".action{now | date "2006-01-02"}"}

- Sum1
- Sum2
}}}
{: name="" fold="0"}
.action{/*s上面设置命名为空和不折叠,为了防止超级块内部的属性错位,被超级块获取*/}
{{{
## WeekGoals
{{SELECT * FROM blocks where alias=".action{$weekResult}" and content="Goals"}}

}}}

}}}

## Recent
> 这三天你内创建的页面如下
.action{$lastThreeDays := now | date_modify "-72h" | date "20060102150405"}
.action{$recent_block := (queryBlocks "SELECT * FROM blocks WHERE box != '?' and box !='思源笔记用户指南' and type='d' and created >'?' order by path " $notebox  $lastThreeDays )}

.action{range $v:= $recent_block}
- ((.action{$v.ID}))	
.action{end}