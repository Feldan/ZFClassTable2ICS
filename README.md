# ZFClassTable2ICS
新版正方教务系统课表生成iCalendar文件`jio`本
> 源码fork自[31415926535x](https://github.com/31415926535x/CollegeProjectBackup/tree/master/ZhengfangClassScheduleToICS)

> 经测试适配于新版正方教务系统。
## 准备工作
- 安装[Tampermonkey](https://www.tampermonkey.net/)
- 安装[ZFClassTable2ICS](https://greasyfork.org/zh-CN/scripts/441136-gdust-%E6%AD%A3%E6%96%B9%E6%95%99%E5%8A%A1%E7%B3%BB%E7%BB%9F%E8%AF%BE%E7%A8%8B%E8%A1%A8%E8%BD%ACics)
## 烹饪过程
**主要修改3个地方**
### 第一 修改教务处系统地址
```js
// ==UserScript==
// @name        GDUST-正方教务系统课程表转ICS
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  通过对新版正方教务系统的课表页面的解析，实现导出一个适用于大部分ics日历的文件，适配与广东科技学院正方教务系统，理论使用于所有使用新版正方教务系统（可对 ``include`` 进行一定的修改以适用不同的学校的链接）
// @author       feldan
// @compatible   chrome
// @compatible   firefox
// @license      MIT
// @include      *://172.16.254.1/* 
// @run-at       document-start
// ==/UserScript==
var ClassScheduleToICSURL = "kbcx/xskbcx_cxXskbcxIndex.html";   // 学生课表查询页面，将该学期的课程信息导出为ics
var ExamScheduleToICSURL = "kwgl/kscx_cxXsksxxIndex.html";      // 考试信息查询页面，将该学期的考试信息导出为ics
var StudentEvalutionURL = "xspjgl/xspj_cxXspjIndex.html";        // 学生评教页面

```
@include
根据自己学校教务系统的网址修改，应该对于新版教务系统的地址都是一样的，故只需修改上面 include中的教务系统的地址即可
### 第二 修改时间
```json
    var TIME = {
        "1": {
            "name": "第1节",
            "startTime": {
                "hour": '08',
                "minute": '30'
            }
        },
        "2": {
            "name": "第2节",
            "startTime": {
                "hour": '09',
                "minute": '20'
            }
    
        },
        "3": {
            "name": "第3节",
            "startTime": {
                "hour": '10',
                "minute": '25'
            },
    
        },
        "4": {
            "name": "第4节",
            "startTime": {
                "hour": '11',
                "minute": '15'
            },
    
        },
        "5": {
            "name": "第5节",
            "startTime": {
                "hour": '14',
                "minute": '40'
            },
    
        },
        "6": {
            "name": "第6节",
            "startTime": {
                "hour": '15',
                "minute": '30'
            },
    
        },
        "7": {
            "name": "第7节",
            "startTime": {
                "hour": '16',
                "minute": '30'
            },
    
        },
        "8": {
            "name": "第8节",
            "startTime": {
                "hour": '17',
                "minute": '20'
            },
    
        },
        "9": {
            "name": "第9节",
            "startTime": {
                "hour": '19',
                "minute": '30'
            },
    
        },
        "10": {
            "name": "第10节",
            "startTime": {
                "hour": '20',
                "minute": '20'
            },
    
        }
    }
```
### 第三 修改提醒时间
```
Calendar.VALARM = "-PT0D0H10M0S";       // 提醒，默认10分钟
                       | |  | |_________秒
                       | |  |___________分
                       | |______________时   
                       |________________天
```
## 食用方法
信息查询 -> 学生课表查询 -> 选择本学期的第一个星期一 -> 生成ICS -> 导入 -> 开恰