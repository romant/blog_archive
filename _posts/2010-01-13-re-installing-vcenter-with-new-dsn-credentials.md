---
ID: 285
post_title: >
  Re-Installing vCenter with new DSN
  credentials
author: Roman Tarnavski
post_date: 2010-01-13 12:57:56
post_excerpt: >
  How to clear MSDB Database jobs so that
  vCenter can re-use the an ODBC
  connection after a previous owner.
layout: post
permalink: >
  http://blog.romant.net/technology/re-installing-vcenter-with-new-dsn-credentials/
published: true
dsq_thread_id:
  - "75453266"
---
If you're ever in a situation where you've moved the vCenter database, and have actually changed the login details for the database that the DSN points to, and you're using SQL Server. Then upon re-installing vCenter, you will be greeted with:
<blockquote>"Database job [Past day stats rollupvcenter] was created by another user. Please use the same user to setup your DSN or remove the job. ODBC Error: [Microsoft][SQL Native Client][SQL Server]The specified @job_name ('Past Day stats rollupvcenter') does not exist.</blockquote>
<a href="http://blog.romant.net/wp-content/uploads/2010/01/vCenter_Install.png"><img class="aligncenter size-large wp-image-293" title="vCenter Install ODBC DSN Error" src="http://blog.romant.net/wp-content/uploads/2010/01/vCenter_Install-600x220.png" alt="" width="600" /></a>

When vCenter is first installed, it schedules jobs with the help of the system DB - MSDB. What's left to do, is just remove the jobs created by the previous dbo of your vCenter data. You achieve this by first listing what jobs are created on the SQL Server.

<code>
SELECT [job_id],
[originating_server_id],
[name],
[enabled],
[description],
[start_step_id],
[category_id],
[owner_sid],
[notify_level_eventlog],
[notify_level_email],
[notify_level_netsend],
[notify_level_page],
[notify_email_operator_id],
[notify_netsend_operator_id],
[notify_page_operator_id],
[delete_level],
[date_created],
[date_modified],
[version_number]
FROM [msdb].[dbo].[sysjobs]
</code>

<a href="http://blog.romant.net/wp-content/uploads/2010/01/sql_server.png"><img class="aligncenter size-large wp-image-287" title="SQL Server Query" src="http://blog.romant.net/wp-content/uploads/2010/01/sql_server-600x493.png" alt="" width="600" /></a>

As you can see, four scheduled operations exist. Thankfully you don't have to worry about just clearing this table, as there's a stored procedure that comes within MSDB -&gt; sp_delete_job

Run it for each of the jobs, and you'll be ready to continue installing vCenter.