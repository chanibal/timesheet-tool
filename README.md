Timesheet tool
==============

Simple time tracking tool.
Parses timesheets, shows summaries.

Usage
-----

```bash
timesheet sheet1.timesheet
```

There is a config variable `showRealTime` that shows non-multiplied time. 
Currently unexposed in switches, must edit source.


Example
-------

```
2021-12-29 10:00-11:00 build something
2021-12-29 11:00-11:30 [bug] [x0] this is on me
2021-12-29 23:00-0:30 [x2] rush job
2021-12-30 10:30-11:30 build something
2021-12-30 16:30-17:30 -||-
2021-12-30 17:30-18:00 another task
```

results in

```
3h00m   build something
0h00m   [bug] [x0] this is on me
3h00m   [x2] rush job
0h30m   another task
-----
6h30m   total
```



Timesheet format
----------------

```
<iso date> <time>-<time> <description> [<optional tag>] <description cont.>
<iso date> <time>-<time> -||-
# comment
```

Where:
- `<iso date>` is a iso-8601 date, ex. `2021-12-29`.
- `<time>` is a hour:minute format time, supports wrapping to the next day (ex. `2021-01-01 23:00-0:30` means `2021-01-01 23:00` to `2021-01-02 0:30`).
- `<description>` is a text description of the task
- `[<optional tag>]` is a special tag that is parsed. Supported tags:
    - `[<number>x]` (ex. `[2x]`) is a hourly multiplier, for those extra i-dont-want-to-do-this jobs.
    - `[feature]`, `[bug]` are parsed, but don't change anything - just markers.

The symbol `-||-` (or it's alias `...`) means repeat previous description and tags.

Changelog
---------

- 2012-06-28 First version in AWK
- 2014-03-12 Javascript rewrite
- 2021-12-29 Documentation, fixes
