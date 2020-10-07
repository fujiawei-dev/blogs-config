---
date: 2020-10-04T19:30:56+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "添加回到顶部的按钮"  # 文章标题
description: "给长文章添加一键回到顶部的按钮。"
url:  "posts/2020/10/04/back2top"  # 设置网页链接，默认使用文件名
tags: [ "hugo"] # 自定义标签
series: [ "博客系统摸爬滚打"]  # 文章主题/文章系列
categories: [ "浅尝辄止"]  # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

index: true  # 文章是否可以被索引
draft:  false  # 草稿
---

{{< code language="html" title="layouts/partials/extended_footer.html" id="1" expand="Show" collapse="Hide" isCollapsed="false" >}}
<script src={{ "assets/back2top.js" | absURL }}></script>

<script>
    addBackToTop({
        diameter: 42,
        backgroundColor: 'rgb(221, 0, 0)',
        textColor: '#fff'
    })
</script>
{{< /code >}}

{{< code language="css" title="layouts/partials/prepended_head.html" id="2" expand="Show" collapse="Hide" isCollapsed="true" >}}
"use strict";
<style>
    #back-to-top {
        background: rgb(221, 0, 0);
        -webkit-border-radius: 50%;
        -moz-border-radius: 50%;
        border-radius: 50%;
        bottom: 20px;
        -webkit-box-shadow: 0 2px 5px 0 rgba(0, 0, 0, .26);
        -moz-box-shadow: 0 2px 5px 0 rgba(0, 0, 0, .26);
        box-shadow: 0 2px 5px 0 rgba(0, 0, 0, .26);
        color: #fff;
        cursor: pointer;
        display: block;
        height: 42px;
        opacity: 1;
        outline: 0;
        position: fixed;
        right: 20px;
        -webkit-tap-highlight-color: transparent;
        -webkit-touch-callout: none;
        -webkit-transition: bottom .2s, opacity .2s;
        -o-transition: bottom .2s, opacity .2s;
        -moz-transition: bottom .2s, opacity .2s;
        transition: bottom .2s, opacity .2s;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        width: 42px;
        z-index: 1
    }

    #back-to-top svg {
        display: block;
        fill: currentColor;
        height: 18px;
        margin: 12px auto 0;
        width: 18px
    }
    
    #back-to-top.hidden {
        bottom: -42px;
        opacity: 0
    }
</style>
{{< /code >}}

{{< code language="js" title="static/assets/back2top.js" id="3" expand="Show" collapse="Hide" isCollapsed="true" >}}
"use strict";

function addBackToTop() {
    var o, t, e, n, i = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {},
        r = i.backgroundColor,
        d = void 0 === r ? "#000" : r,
        a = i.cornerOffset,
        c = void 0 === a ? 20 : a,
        s = i.diameter,
        l = void 0 === s ? 56 : s,
        u = i.ease,
        p = void 0 === u ? function (o) {
            return .5 * (1 - Math.cos(Math.PI * o))
        } : u,
        m = i.id,
        h = void 0 === m ? "back-to-top" : m,
        b = i.innerHTML,
        v = void 0 === b ? '<svg viewBox="0 0 24 24"><path d="M7.41 15.41L12 10.83l4.59 4.58L18 14l-6-6-6 6z"></path></svg>' : b,
        f = i.onClickScrollTo,
        x = void 0 === f ? 0 : f,
        w = i.scrollContainer,
        g = void 0 === w ? document.body : w,
        k = i.scrollDuration,
        y = void 0 === k ? 100 : k,
        T = i.showWhenScrollTopIs,
        M = void 0 === T ? 1 : T,
        z = i.size,
        E = void 0 === z ? l : z,
        C = i.textColor,
        L = void 0 === C ? "#fff" : C,
        N = i.zIndex,
        I = void 0 === N ? 1 : N,
        A = g === document.body,
        B = A && document.documentElement;
    o = Math.round(.43 * E), t = Math.round(.29 * E), e = "#" + h + "{background:" + d + ";-webkit-border-radius:50%;-moz-border-radius:50%;border-radius:50%;bottom:" + c + "px;-webkit-box-shadow:0 2px 5px 0 rgba(0,0,0,.26);-moz-box-shadow:0 2px 5px 0 rgba(0,0,0,.26);box-shadow:0 2px 5px 0 rgba(0,0,0,.26);color:" + L + ";cursor:pointer;display:block;height:" + E + "px;opacity:1;outline:0;position:fixed;right:" + c + "px;-webkit-tap-highlight-color:transparent;-webkit-touch-callout:none;-webkit-transition:bottom .2s,opacity .2s;-o-transition:bottom .2s,opacity .2s;-moz-transition:bottom .2s,opacity .2s;transition:bottom .2s,opacity .2s;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none;width:" + E + "px;z-index:" + I + "}#" + h + " svg{display:block;fill:currentColor;height:" + o + "px;margin:" + t + "px auto 0;width:" + o + "px}#" + h + ".hidden{bottom:-" + E + "px;opacity:0}", (n = document.createElement("style")).appendChild(document.createTextNode(e)), document.head.insertAdjacentElement("afterbegin", n);
    var D = function () {
            var o = document.createElement("div");
            return o.id = h, o.className = "hidden", o.innerHTML = v, o.addEventListener("click", function (o) {
                o.preventDefault(),
                    function () {
                        var o = "function" == typeof x ? x() : x,
                            t = window,
                            e = t.performance,
                            n = t.requestAnimationFrame;
                        if (y <= 0 || void 0 === e || void 0 === n) return q(o);
                        var i = e.now(),
                            r = j(),
                            d = r - o;
                        n(function o(t) {
                            var e = Math.min((t - i) / y, 1);
                            q(r - Math.round(p(e) * d)), e < 1 && n(o)
                        })
                    }()
            }), document.body.appendChild(o), o
        }(),
        H = !0;

    function S() {
        j() >= M ? function () {
            if (!H) return;
            D.className = "", H = !1
        }() : function () {
            if (H) return;
            D.className = "hidden", H = !0
        }()
    }
    
    function j() {
        return g.scrollTop || B && document.documentElement.scrollTop || 0
    }
    
    function q(o) {
        g.scrollTop = o, B && (document.documentElement.scrollTop = o)
    }(A ? window : g).addEventListener("scroll", S), S()
}
{{< /code >}}
