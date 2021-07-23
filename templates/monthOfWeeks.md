.action{/*迭代器*/}
.action{$months := list "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"}
.action{$temp := ""}


.action{range $index ,$month:=$months}

		.action{/*迭代index+1*/}
		.action{$index = add  $index 1}
		
		.action{/*布局*/}
		.action{$setColum:= mod $index 4 }
		.action{if eq $setColum 1}
{{{col
{{{
		.action{else}
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
		
		.action{/*布局*/}
		.action{$setColum:=  mod $index 4 }
		.action{if eq $setColum 0}
}}}
}}}
---
		.action{else}
}}}
		.action{end}
		
.action{end}
