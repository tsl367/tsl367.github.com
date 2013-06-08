---
layout: post
title: "AutoHotky使用点滴"
description: ""
category: 
tags: []
---
{% include JB/setup %}
#AutoHotKey使用点滴
##基本语法
###别名
    ::by the way::by the way
    ::l166::192.168.100.166
###键绑定
####键对应
> "#" 表示Windows键
>  "^" 表示Cntrl键
> "!" 表示Alt
> "+" 表示Shift键
 
##Example
###常用
    #Esc::Send !{F4} ;win+ESC 替换 alt F4
    #f::Run
        https://www.google.com/search?q=%clipboard%
 
    #f::
        current_clipboard = %Clipboard% ; 把目前的剪貼簿內容存起來供後面還原
        Clipboard = ; 先把剪貼簿清空
        Send ^c
        ; 把選取字串用〔Ctrl+C〕存入剪貼簿
        ClipWait, 1 ; 等待1秒讓剪貼簿執行存入動作
        ; 下行使用Google執行搜尋動作，要搜尋的字串就是剪貼簿內容
        Run https://www.google.com/search?q=%Clipboard%
        Clipboard = %current_clipboard% ; 還原先前的剪貼簿內容
        return
 
    #u::Run notepad
    #n::
        Run www.google.com
        Run Notepad.exe
        return
    #a::
        RunWait Notepad ;等到关闭后再运行
        MsgBox The user has finished (Notepad has been closed).
        ^!s::;将选中部分复制，并且alttab切换到另一程序粘贴
        Send ^c!{tab}pasted:^v
        return
###切换程序
    #NoEnv
    SendMode Input
    SetWorkingDir %A_ScriptDir%
    SetTitleMatchMode 2
    ;有六种值 1表示前端匹配；2表示部分匹配；3表示完全匹配；RegEx表示正则
 
    Activate(t)
    {
        IfWinActive,%t%
        {
            WinMinimize
            return
        }
        SetTitleMatchMode 2  
        DetectHiddenWindows,on
        IfWinExist,%t%
        {
            WinShow
            WinActivate         
            return 1
        }
        return 0
    }
 
    ActivateAndOpen(t,p)
    {
        if Activate(t)==0
        {
            Run %p%
            WinActivate
            return
        }
    }
 
    ; Program in common use
    #b::ActivateAndOpen("ahk_class WizNoteMainFrame","D:\ProgramFiles\Wiz\wiz.exe")；由于标题经常变化，可以使用ahk类，用自带的spy来检测
    #3::ActivateAndOpen("ahk_class PuTTY","D:\ProgramFiles\green\putty\putty.exe")；持续按此键，可在putty间切换
    #f::Run
        https://www.google.com/search?q=%clipboard%
    Return
##最大化
    #m::
    {
        WinGetActiveTitle, title
        WinGet, state, MinMax, %title%
        ;state = 1 is Max, -1 Min, 0 other
        if (state)
            WinRestore, %title%
        else
            WinMaximize, %title%
        return
    }
 

