img-lib  
===   

![](https://travis-ci.org/T-phantom/si-img.svg?branch=master)  ![](https://img.shields.io/badge/npm-v1.0.1-blue.svg)   
图片优化插件: 包括图片惰性加载，缓存等功能，图片大小检测，webp格式适配    
主要面向移动端，PC端不支持IE8及以下。    

## 使用   
### 下载源代码：   
> git clone https://github.com/SIPC115/img-lib   

项目中引用 `lib/img.js`, **注意：src中为ES6的开发代码，不建议引入**      

```html  
<script src="img.js"></script>  
```    


### 初始化设置    
在js代码中，我们加入对插件的初始化配置内容
```js  
SI.img({
    lazyWidth: 0,     //预加载当前屏幕以右边lazyWidth内的图片，默认0
    lazyHeight: 0,    //预加载当前屏幕以下lazyHeight内的图片，默认0
    realSrc: "data-src",  //图片路径放置属性
    class: "img-load",    //惰性加载的图片必须的类名
    cachePrefix: "img_cache_url_",    //图片缓存前缀  
    cachePoolName: "img_cache_pool",  //图片缓存池名
    cachePoolLength: 50,              //图片缓存池长度
    wait: 100,                        //节流函数等待时间(谨慎修改)
    fadeIn: null                      //图片显示后调用的函数
})  
```     

### 图片惰性加载    
#### 1. 普通图片
为需要惰性加载的图片添加`img-load`类名，将图片路径写在`data-src`中
```html
<img data-src="http://..." class="img-load">
```     

#### 2. 背景图片  
如果需要对背景图片进行惰性加载，同样可以按照`img`的方式设置，如下：  
```html  
<div data-src="http://....." class="img-load">...</div> 
```  
这种需求很常见，例如移动端商品展示的时候，为了让商品图片没有加载好之前，图片展示位置缩回。通常
用`div`的背景图片做商品图片展示，给一个`padding-top: 100%;`属性就好。 

#### 3. 不同设备做不同区分  
在代码`loadImg`中，我们保留了对图片加载的判断接口(使用者可以根据网络环境，设备等问题，考虑是否开启惰性加载)    

### 图片缓存  
将需要缓存的图片加上`data-cache=1`的属性  
```html  
<img data-cache=1 data-src="http://....." class="img-load">  
```  
这样的图片信息在首次加载完毕后，会以base64的格式存储在`localStorage`中，下次加载页面时，会直接拉去`localStorage`
中的图片数据。使用图片缓存需要注意一下问题：  

* 缓存图片的数量默认为50，请保证你缓存的图片总大小不会超过 `localStorage`容量上限    
* 注意缓存的图片被自动打上 `crossOrigin="anonymous" `属性（如果你的开启图片共享有可能存在安全问题，不建议开启）。    

### webp格式替换  
目前`src`中的代码引入了，对webp图片格式的探测。因为webp格式目前只能在chrome中使用，所以需要有专门的图片地址
来提供webp格式图片。这部分内容需要在实际应用中调整。     

### 图片的优化   
暂未正式使用  

## DEMO 地址  
[示例demo](/test/index.html)  

## Changelog    
### 1.0.0  
1. 完成组件的基本架构  
2. 完成图片惰性加载功能  
3. 完成图片base64缓存功能    

### 1.0.1  
1. 修复背景图片加载失败的BUG  












