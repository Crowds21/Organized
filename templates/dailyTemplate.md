.action{/*获取当前是第几周*/}
	.action{$ng_duration := (toDate "2006-01-02" "2021-01-01").Sub now}
	.action{$weekhours:=mul 7 24}
	.action{$duration:=sub 0 $ng_duration.Hours }
	.action{$week := div $duration $weekhours}
	.action{$today:= (now | date "2006-01")}
	.action{$weekResult:= (list $today "Week" $week| join " ")}


# .action{now | date "2006-01-02"}Diary
{: alias=".action{$weekResult}"}

## Summary-Yesterday
.action{$yesterday:=(now | date_modify "-24h") | date "2006-01-02"}
{{select * from blocks where  box like 'DailySchedule'  and type='h' and  content = 'Summary' and path like '%.action{$yesterday}%'}}


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

{{{
## WeekGoals
{{SELECT * FROM blocks where alias=".action{$weekResult}" and content="Goals"}}

}}}

}}}