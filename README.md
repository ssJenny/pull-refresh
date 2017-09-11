# pull-refresh

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


# 安装依赖 vue-scroller

npm install --save vue-scroller

引入到相应组件
import VueScroller from 'vue-scroller'
Vue.use(VueScroller)

此插件的标签为scroller

```
<scroller :on-infinite="infinite" :on-refresh="refresh" ref="myscroll">
      ...
</scroller>
```

下拉刷新
```
refresh(done) {
  setTimeout(() => {
    let start = this.top - 1
    for(let i = start; i > start - 10; i--) {
      this.data.splice(0,0, i)
    }
    this.top = this.top - 10;
    done()
  }, 1500)
}
```
上拉刷新
```
infinite(done){
  if(this.noData) {
    setTimeout(() => {
    // 没有数据时的处理函数
      this.$refs.myscroll.finishInfinite(2);
    })
    return;
  }
  let self = this;
  let start = this.data.length;

  setTimeout( () => {
    for(let i = start + 1; i < start + 10; i++){
      self.data.push(i)
    }
    if(start >  30){
      self.noData = "没有更多数据"
    }

    self.$refs.myscroll.resize();

    done()
  }, 1500)
}
```
