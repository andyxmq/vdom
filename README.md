# vdom
vitual-dom

## 核心函数API

- h('<标签名>', {属性名...}, [...子元素...])
- h('<标签名>' {属性名...}, '...')

- patch(container,vnode)
- patch(vnode, newVnode)

## diff算法 vdom为什么使用diff算法 diff算法的实现流程

> diff算法的实现流程

1. DOM操作是昂贵的、因此尽量减少DOM操作
2. 找出本次DOM必须更新的节点来更新，其它的不更新
3. 这个找出过程 就需要diff算法 

> diff实现（两个核心点）

1. patch(container, vnode)

  vnode -> dom (实现3)
```js 
  function createElement(vnode) {
    // vode = {tag,attr,children}
    var tag = vnode.tag;
    var attrs = vnode.attrs || {};
    var children = vnode.children || [];

    if(tag === null){
      return null
    }

    // 创建元素
    var elem = document.createElement(tag);
    
    //属性
    var attrName
    for(attrName in attrs){
      if(attrs.hasOwnProperty(attrName)){
        elem.setAttribute(attrName, attrs[attrs])
      }
    }

    // 子元素
    children.forEach(function(childNode){
      // 给elem 添加子元素
      elem.append(createElement(childNode)) 
    })
    return elem;
  }
```
2. patch(vnode, newVnode)