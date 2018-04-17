# koa2 加载中间件方法

## 基本用法



#### Koa2 启动脚本
```js
import { join } from 'path'
import Koa from 'koa'
import R from 'ramda'
import chalk from 'chalk'
import config from '../config'

const MIDDLEWARES = ['general', 'router']
const useMiddlewares = (app) => {
  R.map(
    R.compose(
      R.forEachObjIndexed(
        e => e(app)
      ),
      require,
      name => join(__dirname, `./middleware/${name}`)
    )
  )(MIDDLEWARES)

async function start () {
  const app = new Koa()
  const { port } = config

  await useMiddlewares(app)

  const server = app.listen(port, () => {

  })
}

start()
```

