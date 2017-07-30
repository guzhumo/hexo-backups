---
title: rem页面布局
date: 2017-07-28 14:22:45
categories: layout
tags: rem
---
### 注意
>**绝不是每个地方都要用rem，rem只适用于固定尺寸！**
在相当数量的布局情境中（比如底部导航元素平分屏幕宽，大尺寸元素），你必须使用百分比或者flex才能完美布局！

### 常用手机尺寸
- iphone5 320 * 2 = 640px
- iphone6 375 * 2 = 750px
- iphone6s 414 * 3 = 1242px

### 问：高清方案在微信上，有时候字体会不受控制变的很大，怎么办？
>问题原因：
在X5新内核Blink中，在排版页面的时候，会主动对字体进行放大，会检测页面中的主字体，当某一块字体在
我们的判定规则中，认为字号较小，并且是页面中的主要字体，就会采取主动放大的操作。然而这不是我们想要的，可以采取给最大高度解决
>解决方案：
```
*, *:before, *:after { max-height: 100000px }
```
>后续：经过项目实践，还是决定给 max-height 一个具体数值比较好，之前给的是 100% ，但有自身的局限性，比如 antd 的轮播组件在 max-height:100% 的情况下就不能正常显示。
>补充：有同学反映，在一些情况下 textarea 标签内的字体大小即便加上上面的方案，字体也会变大，无法控制。此时你需要给 textarea 的 display 设为 table 或者 inline-table 即可恢复正常。（感谢 程序媛喵喵 对此的补充）


### 源码解读
```
~function () {
            var winW = document.documentElement.clientWidth,
                    desW = 640;
            if (winW < desW) {/*超过设计稿,最大就按照设计稿的尺寸即可*/
                document.documentElement.style.fontSize = winW / desW * 100 + 'px';
            }
        }();
```
> 基本适合任何移动设备
```
'use strict';

/**
 * @param {Number} [baseFontSize = 100] - 基础fontSize, 默认100px;
 * @param {Number} [fontscale = 1] - 有的业务希望能放大一定比例的字体;
 */
const win = window;
export default win.flex = (baseFontSize, fontscale) => {
  const _baseFontSize = baseFontSize || 100;
  const _fontscale = fontscale || 1;

  const doc = win.document;
  const ua = navigator.userAgent;
  const matches = ua.match(/Android[\S\s]+AppleWebkit\/(\d{3})/i);
  const UCversion = ua.match(/U3\/((\d+|\.){5,})/i);
  const isUCHd = UCversion && parseInt(UCversion[1].split('.').join(''), 10) >= 80;
  const isIos = navigator.appVersion.match(/(iphone|ipad|ipod)/gi);
  let dpr = win.devicePixelRatio || 1;
  if (!isIos && !(matches && matches[1] > 534) && !isUCHd) {
    // 如果非iOS, 非Android4.3以上, 非UC内核, 就不执行高清, dpr设为1;
    dpr = 1;
  }
  const scale = 1 / dpr;

  let metaEl = doc.querySelector('meta[name="viewport"]');
  if (!metaEl) {
    metaEl = doc.createElement('meta');
    metaEl.setAttribute('name', 'viewport');
    doc.head.appendChild(metaEl);
  }
  metaEl.setAttribute('content', `width=device-width,user-scalable=no,initial-scale=${scale},maximum-scale=${scale},minimum-scale=${scale}`);
  doc.documentElement.style.fontSize = `${_baseFontSize / 2 * dpr * _fontscale}px`;
};
```
