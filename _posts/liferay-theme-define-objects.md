title: <liferay-theme:defineObjects />
date: 2014-05-04 21:32:39
categories: liferay
tags: [liferay, tags]
description: <liferay-theme:defineObjects />
keywords: liferay, tags
---
> 在jsp中添加`<liferay-theme:defineObjects />`之后，可以使用的对象。

``` java
ThemeDisplay themeDisplay
Company company
Account account
User user
User realUser
Contact contact
Layout layout
List<Layout> layouts
long plid
LayoutTypePortlet layoutTypePortlet
long scopeGroupId
PermissionChecker permissionChecker
Locale locale
TimeZone timeZone
Theme theme
ColorScheme colorScheme
PortletDisplay portletDisplay
long portletGroupId
```
<!--more-->
其核心就只有themeDisplay，其余都是通过themeDisplay获得的。以下为`DefineObjectsTag.java`部分源码。
``` java
@Override
public int doStartTag() {
    HttpServletRequest request = (HttpServletRequest) pageContext.getRequest();

    ThemeDisplay themeDisplay = (ThemeDisplay) request.getAttribute(WebKeys.THEME_DISPLAY);

    if (themeDisplay != null) {
        pageContext.setAttribute("themeDisplay", themeDisplay);
        pageContext.setAttribute("company", themeDisplay.getCompany());
        pageContext.setAttribute("account", themeDisplay.getAccount());
        pageContext.setAttribute("user", themeDisplay.getUser());
        pageContext.setAttribute("realUser", themeDisplay.getRealUser());
        pageContext.setAttribute("contact", themeDisplay.getContact());

        if (themeDisplay.getLayout() != null) {
            pageContext.setAttribute("layout", themeDisplay.getLayout());
        }

        if (themeDisplay.getLayouts() != null) {
            pageContext.setAttribute("layouts", themeDisplay.getLayouts());
        }

        pageContext.setAttribute("plid", new Long(themeDisplay.getPlid()));

        if (themeDisplay.getLayoutTypePortlet() != null) {
            pageContext.setAttribute("layoutTypePortlet", themeDisplay.getLayoutTypePortlet());
        }

        pageContext.setAttribute("scopeGroupId", new Long(themeDisplay.getScopeGroupId()));
        pageContext.setAttribute("permissionChecker", themeDisplay.getPermissionChecker());
        pageContext.setAttribute("locale", themeDisplay.getLocale());
        pageContext.setAttribute("timeZone", themeDisplay.getTimeZone());
        pageContext.setAttribute("theme", themeDisplay.getTheme());
        pageContext.setAttribute("colorScheme", themeDisplay.getColorScheme());
        pageContext.setAttribute("portletDisplay", themeDisplay.getPortletDisplay());

        // Deprecated

        pageContext.setAttribute("portletGroupId", new Long(themeDisplay.getScopeGroupId()));
    }

    return SKIP_BODY;
}
```

### 参考文献
1. [Portlet:DefineObjects tag in jsp](http://www.liferay.com/zh/community/forums/-/message_boards/message/5997940)
2. [liferay 在jsp中直接使用的对象](http://blog.csdn.net/wenyitao880901/article/details/6181129)

--**EOF**--