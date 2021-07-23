
.action{/*获取星期*/}
	.action{/*距离周一的天数*/}
	.action{$ng_day_of_week := mod (div ((toDate "2006-01-02" "2021-06-28").Sub now).Hours 24) 7 }
	.action{/*将天数转换为正数*/}
	.action{$day_of_week := sub 0 $ng_day_of_week}
	.action{/*结果*/}
	.action{$day_of_week_result := last (slice (list "星期一" "星期二" "星期三" "星期四" "星期五" "星期六" "星期日") 0   $day_of_week )}
	
	
	
.action{/*获取当前是第几周*/}
	.action{/*距离01-01的小时数(负数)*/}
	.action{$ng_duration := (toDate "2006-01-02" "2021-01-01").Sub now}
	.action{/*一星期的小时数*/}	
	.action{$weekhours:=mul 7 24}
	.action{/*将距离1-1的小时数转换为正数*/}			
	.action{$duration:=sub 0 $ng_duration.Hours }
	.action{/*取整*/}
	.action{$week := div $duration $weekhours}
	.action{/*今天的日期*/}
	.action{$today:= (now | date "2006-01")}
	.action{/*生成想要的字符串*/}
	.action{$weekResult:= (list $today "Week" $week| join " ")}


.action{/*循环生成星期列表*/}
	.action{/*今天距离周一有几天*/}
	.action{$week := (mod (div ((toDate "2006-01-02" "2021-06-28").Sub now).Hours 24) 7) }
	.action{/*生成周一日期所需要修正的时长*/}
	.action{$monday:= mul 24 $week}
	.action{/*用于range循环,表示循环7次, 没什么实际意义*/}
	.action{$days := list "星期一" "星期二" "星期三" "星期四" "星期五" "星期六" "星期日"}
	.action{range $index,$day:=$days}

		.action{/*迭代 每次增加24*/}
		.action{$after := mul 24 $index}
		.action{/*在周一的基础上,附加的时间*/}
		.action{$realdate:= add $monday $after}
		.action{/*生成以 h 为单位的 字符串*/}
		.action{$result:=(list $realdate "h" | join "")}
		.action{/*获取列表项*/}
		.action{$days_list := now | date_modify $result  | date "2006-01-02"}
		
		.action{/*输出日期*/}
		.action{$days_list}  
		.action{/*输出星期*/}
		.action{last (slice (list "星期一" "星期二" "星期三" "星期四" "星期五" "星期六" "星期日") 0 (add 1 $index ) )}

		.action{/*在下方输入需要的SQL语句或其他*/}
		
		.action{/*迭代index+1/}
		.action{$index := add  $index 1}
	.action{end}
	
	
	

.action{/*生成WeekGoals的列表项*/}
	.action{/*迭代器*/}
	.action{$months := list "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"}
	.action{$temp := ""}

	.action{range $index ,$month:=$months}

		.action{/*迭代令index初始为1*/}
		.action{$index = add  $index 1}
		
		.action{/*列布局的开始*/}
		.action{$setColum:= mod $index 4 }
		.action{if eq $setColum 1}
			.action{/*一个新的超级块*/}
			{{{col
			{{{
		.action{else}
			.action{/*同一个超级块中的另一列*/}
			{{{
		.action{end}
		
			#### .action{$month}
		
		.action{/*生成年份*/}
		.action{$year:= ( now| date "2006")}
		
		.action{/*生成月份*/}
		.action{if lt $index 10}
			.action{$temp =(list " " $index | join "0")}
			.action{$temp = trim $temp}	
		.action{else}
			.action{$temp = $index}
		.action{end}
		
		.action{$result:=(list $year $temp | join "-")}
		.action{$result =(list $result "Week" | join " ")}
		
		.action{$block := (queryBlocks "select * from blocks where type='d' and content like '%?%' order by content" $result )}
		.action{range $v:= $block}
			- ((.action{$v.ID}))
		.action{end}
		
		.action{/*列布局的末尾*/}
		.action{$setColum:=  mod $index 4 }
		.action{if eq $setColum 0}
			.action{/*一个超级块的结束*/}
			}}}
			}}}
			---
		.action{else}
			.action{/*一列的结束*/}
			}}}
		.action{end}
		
.action{end}



