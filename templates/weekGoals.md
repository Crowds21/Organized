.action{$ng_duration := (toDate "2006-01-02" "2021-01-01").Sub now}
.action{$weekhours:=mul 7 24}
.action{$duration:=sub 0 $ng_duration.Hours }
.action{$week := div $duration $weekhours}
.action{$today:= (now | date "2006-01")}
.action{$weekResult:= (list $today "Week" $week| join " ")}


# .action{$weekResult}

## Goals
{: alias=".action{$weekResult}"}
- Task1
- Task2


## Days

.action{/*今天距离周一有几天*/}
.action{$ng_week := (mod (div ((toDate "2006-01-02" "2021-06-28").Sub now).Hours 24) 7) }

.action{/*用于range循环,表示循环7次, 没什么实际意义*/}
.action{$days := list "星期六" "星期五" "星期四" "星期三" "星期二" "星期一" "星期天"}


.action{/*循环生成星期列表*/}
.action{/*生成周一日期所需要修正的时长*/}
.action{$monday:= mul 24 $ng_week}

{{{col
.action{range $index,$day:=$days}

.action{/*布局*/}
.action{$setColum:= mod (add $index 1) 4 }
.action{if eq $setColum 1}
{{{
.action{end}


.action{/*迭代 每次增加24*/}
.action{$after := mul 24 $index}
.action{/*在周一的基础上,附加的时间*/}
.action{$realdate:= add $monday $after}
.action{/*生成以 h 为单位的 字符串*/}
.action{$result:=(list $realdate "h" | join "")}
.action{/*获取列表项*/}
.action{$days_list := now | date_modify $result  | date "2006-01-02"}
	
###### .action{$days_list}  .action{last (slice (list "星期一" "星期二" "星期三" "星期四" "星期五" "星期六" "星期日") 0 (add 1 $index ) )}

{{select * from blocks where name=".action{$days_list}" and content="Schedule" }}


.action{/*布局*/}
.action{$setColum:= mod (add $index 1) 4 }
.action{if eq $setColum 0}
}}}
.action{else if eq $index 6}
}}}
.action{end}

.action{$index := add  $index 1}
.action{end}

}}}

## Weekly Summary
{{SELECT * from blocks where type='h' and  content = 'Summary' and alias='.action{$weekResult}' }}