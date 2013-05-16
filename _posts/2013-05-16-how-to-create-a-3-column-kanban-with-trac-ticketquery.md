---
layout: post
title: "how to create a 3 column kanban with trac TicketQuery"
description: ""
category: kanban scrum
tags: [trac]
---
{% include JB/setup %}

使用Trac 1.0的TicketQuery即可再wiki页面中展示出ticket查询的动态内容，结合使用div布局可以实现多列的看板。
下面的例子实现了一个3列的看板。（注意trac 1.0以前的版本不支持此功能）。

== 搜索产品-q2-迭代3看板  ==

```

{{{
#!div style="float:left; margin-right:1em; width:30%;color:blue"

= Open Tickets = 

Total: [[TicketQuery(status=new|reopened,milestone=搜索产品-q2-迭代3,format=count)]] 

[[TicketQuery(group=priority,status=new|reopened,milestone=搜索产品-q2-迭代3)]]

}}}
{{{
#!div style="float:left; margin-right:1em; width:30%;color:#FF9900" 

= Work In Progress =

Total: [[TicketQuery(status=accepted|testable,milestone=搜索产品-q2-迭代3,format=count)]] 

== Started ==

[[TicketQuery(status=accepted,order=priority,group=owner,milestone=搜索产品-q2-迭代3)]]

== Ready for Test ==

[[TicketQuery(status=testable&review_issues=0&reviewed!=,group=developertest,milestone=搜索产品-q2-迭代3)]]

== Reviewed tickets with issues ==

[[TicketQuery(review_issues=1,group=owner,status=testable|closed,resolution=fixed,milestone=搜索产品-q2-迭代3)]]

== Unreviewed tickets == 

[[TicketQuery(review_issues!=1,status=closed|testable,group=status,resolution=fixed,reviewed=,milestone=搜索产品-q2-迭代3)]]


}}}
{{{
#!div style="float:left; margin-right:1em; width:30%;color:#CC0033" 


= Closed Tickets = 

Total fixed: [[TicketQuery(status=closed,milestone=搜索产品-q2-迭代3,resolution=fixed,format=count)]] 
Other: [[TicketQuery(status=closed,milestone=搜索产品-q2-迭代3,resolution!=fixed,format=count)]] 

== Fixed tickets ==

[[TicketQuery(status=closed,group=type,resolution=fixed,milestone=搜索产品-q2-迭代3)]]

== Other resolutions ==

[[TicketQuery(status=closed,group=resolution,resolution!=fixed,milestone=搜索产品-q2-迭代3)]]


}}}

{{{
#!div style="clear:both"
}}}

```