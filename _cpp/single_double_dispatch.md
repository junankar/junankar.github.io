---
title: "Single and Double Dispatch"
permalink: /cpp/dispatch/
last_modified_at: 2020-07-27
---

# Single Dispatch

> Mechanism where the choice of which version of a method to call is based on the type of a single object.

<details><summary>Click to expand C++ Code</summary>
<p>
<code>
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fjunankar%2FCPP%2Fblob%2Fmain%2FSingle_Disptach.cpp&style=vs2015&showBorder=on"></script>
</code>
</p>
</details>

Reference: [Wiki](https://en.wikipedia.org/wiki/Dynamic_dispatch#Single_and_multiple_dispatch)
 
# Double Dispatch

> Mechanism that dispatches a function call to different concrete functions depending on the runtime types of two objects involved in the call.  

Reference: [Wiki](https://en.wikipedia.org/wiki/Double_dispatch)  

Visitor design pattern is good example of using double dispatch where concrete function is selected on basis of concrete visitor and concrete element types.

# References:

* [Double dispatch in C++](https://en.wikipedia.org/wiki/Double_dispatch#Double_dispatch_in_C++)
* [Stop reimplementing the virtual table and start using double dispatch](https://gieseanw.wordpress.com/2018/12/29/stop-reimplementing-the-virtual-table-and-start-using-double-dispatch/)
* [Multiple Dispatch A new approach using templates and RTTI](http://www.eptacom.net/pubblicazioni/pub_eng/mdisp.html)
