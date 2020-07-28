---
layout: post
author: Tom Fynes
title: Always On Operator Alerts
date: 2020-03-18T09:00:00.000Z
thumbnail: /assets/img/posts/Operators/Cover.png
category: TSQL
summary: Adding alerts for the SQL agent operator.
---

Operator alerts are great right? They are a free feature to let you know that something potentially awful is going on with your server and that being said if you are using Always On what is better then an extra layer of alerting.

If you would like to add some alerts around always on you can use the following script:

{% highlight ruby %}
IF (SELECT SERVERPROPERTY ('IsHadrEnabled')) = 1 BEGIN

    if (select count (*) from msdb.dbo.sysalerts where                 
    name = N'Hadr - Role Change') < 1 begin
        EXEC msdb.dbo.sp_add_alert @name=N'Hadr - Role Change',
        @message_id=1480,
        @severity=0,
        @enabled=1,
        @delay_between_responses=60,
        @include_event_description_in=1,
        @job_id=N'00000000-0000-0000-0000-000000000000'
        print 'Hadr - Role Change alert has been created'
    End
    
    if (select count (*) from msdb.dbo.sysalerts where 
    name = N'Hadr Data Movement Suspended') < 1 begin
        EXEC msdb.dbo.sp_add_alert
        @name=N'Hadr - Data Movement Suspended',
        @message_id=35264,
        @severity=0,
        @enabled=1,
        @delay_between_responses=60,
        @include_event_description_in=1,
        @job_id=N'00000000-0000-0000-0000-000000000000'
        print 'Hadr Data Movement Suspended alert has been created'
    END

    if (select count (*) from msdb.dbo.sysalerts where 
    name = N'Hadr - Data Movement Resumed') < 1 begin
        EXEC msdb.dbo.sp_add_alert
        @name=N'Hadr - Data Movement Resumed',
        @message_id=35265,
        @severity=0,
        @enabled=1,
        @delay_between_responses=60,
        @include_event_description_in=1,
        @job_id=N'00000000-0000-0000-0000-000000000000'
        print 'Hadr Data Movement Resumed alert has been created'
    END
END
{% endhighlight %}

That being said, if you are like me and you have a management database, I have created a stored proc to not only create the always on alerts but also some stock alerts that I think every server should have along with assigning these to an operator and agent jobs. Bit of a disclaimer some of the alerts are from the script you can find on Brent Ozars [website][Website] but I have adapted this for use in my stored proc which you can find [here][Proc].  




[Website]: https://www.brentozar.com/blitz/configure-sql-server-alerts/
[Proc]:   https://github.com/Tom-Fynes/SP_CreateAndEnableFailureAlerts
