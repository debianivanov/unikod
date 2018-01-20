# u m - z p r o c

## D E S C R I P T I O N

```

Create a custom Zabbix template for monitoring certain process.

You want to create Zabbix templates for monitoring various processes your
operating system is running. For example, you want to add one Zabbix template
for monitoring Apache HTTPD and one for MySQL, because you are running a web
site.

It is cumbersome to create Zabbix templates from scratch and put items in them
manually, so I developed a program to bring some automation to the process.

In most cases you want to monitor many aspects of a service, e.g., number of
processes, CPU or memory usage, but you have to do a lot of clicking through
the interface in order to get things done, especially for a large number of
services.

```

## U S A G E

```

I have added an example template ZBX-tmplt-lvl2-Linux-process-Sample-server,
which you will be using as a basis for certain process. Download the XML file
provided in this directory and import it in your Zabbix server installation
(from Configuration => Templates => Import).

Now you need to click on the template name and select Full clone.

Rename this full copy of the template, for example to
ZBX-tmplt-lvl1-Linux-process-PostgreSQL-server, and click Add.

All you have to remember is the template ID, which can be found in the address
bar, when you click on the name of your template, e.g., templateid=10114.

Finally, execute the following command:

./um-zproc \
--itemname='PostgreSQL' \
--procname='postgres' \
--procuser='postgres' \
--procchild='^postgres:' \
--procparent='^/usr/lib/postgresql/.../bin/postgres' \
--hostid='10114'

Note that --procchild and --procparent are regex patterns and must be
different from each other.

Refresh Zabbix. You will see your template populated with the data above and
ready for PostgreSQL process monitoring.

```

## F E A T U R E S

```

Currently this tool supports the following items and several default triggers:
    • number of child processes
    • number of max processes
    • number of parent processes
    • resource usage: child / parent processes memory RSZ avg / max / min / sum
      [ B ] (resident set size)
    • resource usage: child / parent processes memory SSZ avg / max / min / sum
      [ B ] (swap set size)
    • resource usage: child / parent processes memory VSZ avg / max / min / sum
      [ B ] (virtual set size)

```

## T O - D O

```

In the to-do list there are the following tasks:
    • CPU system and user usage
    • shared memory usage

```

## B U G S

```

Number of max processes must be explicitly defined as a custom user parameter.

There is no proper error handling.

There needs to be a more meaningful help included in the script.

This utility works directly with the database (only PostgreSQL at this time)
and not through a Zabbix API library.

```

