# webpack 系列

### 多页面配置优化

最近接手的一个公司项目编译构建速度非常的慢，打包在70s+，修改代码后的重新编译在20s以上（这还属于最快的时候，慢的时候打包100s+，说多了都是泪）

在我不懈的努力的下，终于将打包速度降到20s左右，重新编译在10s左右

原来的配置是webpack:v1.14.0、html-webpack-plugin:v2.22.0

速度慢是主要是因为html-webpack-plugin，这个项目大概有180个页面，多页面会导致速度急剧下降，后来在github某个[issue](https://github.com/jantimon/html-webpack-plugin/issues/724)上找到了原因

根据作者的回答，2.x的版本采用了webpack提供的模版，这导致了速度的下降
> the 2.x branch is using the webpack compiler to provide more flexibility about the templating. Unfortunately the underlying webpack api required some work arounds which seem to be really slow for newer webpack versions. Especially in larger projects

将webpack升级到2.x，html-webpack-plugin下降到1.70，问题解决

别看我写的少，花了我好几天的时间，先升级到webpack 4，发现速度降到了40s，仍然没有达到我的预期，然后再降到2，折腾了好久... 下周出一个webpack系列

未来待续...