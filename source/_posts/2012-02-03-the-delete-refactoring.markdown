---
layout: post
title: "The Delete Refactoring"
date: 2012-02-03 11:22
comments: true
categories: patterns refactoring
---

<p style="text-align: center;">The Code is unnecessary.</p>
<p style="text-align: center;"><em>Delete it.</em></p>

    void printLog (String msg) {                   
        int logLevel = 2;                   
        LOG.printLine(msg);          
    }        
    
<p style="text-align: center;">=></p>
    
    void printLog (String msg) {                   
        LOG.printLine(msg);          
    }    

## Motivation    

Sometimes code doesn't do anything.  Maybe a variable is no longer used, or a
whole function or class is no longer referenced by the rest of the code.  If
that happens, delete it.    

## Mechanics    

* select unused code  
* press the delete key  
* compile and test    

## Example    

I start with the following code:            

    // This method is no longer used          
    // int getErrorLevel() {          
    //     return -1;          
    // }    
    
Select the text and hit delete.  I now have the resulting code:

<p>&nbsp;</p>
