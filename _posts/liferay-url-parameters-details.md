title: Liferay URL parameters details 
date: 2014-04-08 21:54:29
categories: liferay
tags: [liferay, url, parameter]
description: Liferay URL parameters details 
keywords: liferay, url, parameter
---
本文将介绍lifeary url中的部分参数含义。转自[Liferay URL parameters details](http://www.liferaysolution.com/2011/09/liferay-url-parameters-details.html)。

1. `p_p_id`: this parameter is used to tell which portlet to access.
2. `p_p_lifecycle`: this parameter is used in telling Liferay which action to perform. This is a binary value (0 or 1). 0 simply tells Liferay to just render the portlet, whereas 1 tells Liferay to call the process Method of a StrutsAction.
3. `p_p_state`: this parameter is a unique parameter, in that, it is used in helping with Liferay pop ups and AJAX calls. In the current URL above, the parameter is set to normal, therefore, everything is rendered as it should. This parameter also has other values, such as exclusive, maximized and minimized.
	**exclusive** state tells the page to ONLY render that particular portlet
    **maximized** state is used in telling liferay to render the portlet (when placed on a page) in full, works kinda like if you were to have a collapsible div in javascript.The display below shows you what adding a new Web Content Display looks like. Surrounding this display item there is a border with a few buttons to click on to perform actions for this particular portlet. This is to demonstrate the Maximized and Minimized States for a portlet. Clicking on the Minus sign will collapse the div, whereas, clicking on the Plus sign will Maximize the div.
    **minimized** state (shown above) is used to display the portlet collapsed.
4. `p_p_mode`: this parameter acts as a Struts Action parameter. Just like a switch statement in PHP, this parameter is used to tell which Struts Method to render. This is mainly seen/used while in the control panel when you are editing a created page or editing your personal profile.
5. `p_p_col_id` and `p_p_col_count`: these parameters are used in aiding the Liferay templating system.

### 参考文献
1. [Liferay URL parameters details](http://www.liferaysolution.com/2011/09/liferay-url-parameters-details.html)

---
全文完