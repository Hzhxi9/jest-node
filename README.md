### JestNode

前端自动化测试学习笔记

### Link

1. [技术胖-一起学习前端自动化测试](http://www.jspang.com/detailed?id=65)
2. [Jest (一个令人愉快的 JavaScript 测试框架)，目前最流行的前端测试框架，几乎国内所有的大型互联网公司都在使用](https://www.jestjs.cn/)
3. [Mocha (简单, 灵活, 有趣)，它是一个功能丰富的 JavaScript 测试框架，运行在 Node.js 和浏览器中，使异步测试变得简单有趣](https://mochajs.cn/)
4. [Jasmine (BDD-集成测试开发框架) ](https://jasmine.github.io/)
5. [Jest 匹配器](https://jestjs.io/docs/en/expect)

## 单元测试和集成测试的区别

1. **单元测试**：英文是(unit testing)，是指对软件中的最小可测试单元进行检查和验证。前端所说的单元测试就是对一个模块进行测试。也就是说前端测试的时候，你测试的东西一定是一个模块。

2. **集成测试**：也叫组装测试或者联合测试。在单元测试的基础上，将所有模块按照涉及要求组装成为子系统或系统，进行集成测试。

## Jest

#### 优点

1. 比较新
2. 基础好 (性能好，上手简单，功能多)
3. 速度快 (有单独模块测试，比如说有两个模块 A 和 B，以前都测试过了，这时候你只改动 A 模块，才次测试，模块 B 不会再跑一次，而是直接测试 A 模块。)
4. Api 简单，数量少
5. 隔离性好(测试文件单独隔离，这样就避免不同的测试文件执行的时候互相影响而造成出错。)
6. IDE 整合
7. 多项目运行（并行测试，比如我们写了 Node.js 的后台项目，用 React 写了一个前台项目，Jest 是支持他们并行运行，让我们的效率更加提高了）
8. 覆盖率(一键导出测试覆盖率，对于一个项目的测试都要出覆盖率的，Jest 就可以快速出这样的覆盖率统计结果，非常好用)

#### 环境搭建

1.  `yarn add --dev jest`
2.  `npm install --save-dev jest`

#### 初始化配置

1. 初始化命令 `npx jest --init`
2. 配置选择
   - Choose the test environment that will be used for testing?(代码是运行在 Node 环境还是 Web 环境下？) node / jsdom
   - Do you want Jest to add coverage reports?(是否生成测试覆盖率) yes
   - Automatically clear mock calls and instrances between every test?(是否需要在测试之后清楚模拟调用的一些东西？) yes
   - 在这三个选项选择之后，你会发现你的工程根目录下多了一个`jest.config.js`的文件。打开文件你可以看到里边有很多 Jest 的配置项。
3. coverageDirectory 详解
   - `code coverage` 代码测试覆盖率，就是我们测试代码对功能性代码和业务逻辑代码做了百分多少的测试，这个百分比就是代码测试覆盖率
   - `coverageDirectory : "coverage"` 用来打开代码覆盖率
   - `npx jest --coverage` 命令自动生成代码测试覆盖率的说明
   - 生成的`coverage`文件夹可以打开`coverage-lcov-reporrt/index.html`查看网页形式的测试覆盖率报告

#### 开启自动测试

通过配置`package.json`文件设置， `test: "jest --watchAll"`

#### Jest 中的匹配器

| 匹配器                     | 备注                                                                                                                   |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `toBe()`                   | 简单理解就是相等，等同于`===`，也就是严格相等                                                                          |
| `toEqual()`                | 内容相等，不严格匹配但要求值相等时使用                                                                                 |
| `toBeNull()`               | 只匹配`null`值，不匹配`undefined`值                                                                                    |
| `toBeUndefined()`          | 只匹配`undefined`值                                                                                                    |
| `toBeDefined()`            | 匹配定义过的值，注意定义一个`null`值也是通过测试的                                                                     |
| `toBeTruthy()`             | 匹配`true`和`false`,相当于判断真假                                                                                     |
| `toBeFalsy()`              | 与`toBeTruthy`相反，返回`false`就可以通过测试                                                                          |
| `toBeGreaterThan()`        | 匹配大于`>`                                                                                                            |
| `toBeLessThan()`           | 匹配小于`<`                                                                                                            |
| `toBeGreaterThanOrEqual()` | 匹配大于等于`>=`                                                                                                       |
| `toBeLessThanOrEqual()`    | 匹配小于等于`<=`                                                                                                       |
| `toBeCloseTo()`            | 自动消除`JavaScript`浮点精度错误                                                                                       |
| `toMatch()`                | 字符串包含匹配器                                                                                                       |
| `toContain()`              | 数组包含匹配器，完美兼容`Set`对象                                                                                      |
| `toThrow()`                | 专门对异常进行处理，可以检测一个方法会不会抛出异常，<br>也可以在匹配器中加一些字符串，表示抛出的异常必须和字符串相对应 |
| `not`                      | 表示相反或者取反                                                                                                       |

#### 让 Jest 支持 import 和 ES6 语法

目前 Jest 不支持`import ... from ...`这种形式， 因为 Jest 默认支持的是`CommonJS`规范，也就是`NodeJS`中的语法，只支持`require`这种引用

想要使用`import`和 ES6 的语法，需要用 Babel 进行转换

#### 安装 Babel 转换器

> `npm install @babel/core@7.4.5 @babel/preset-env@7.4.5 -D`

> `yarn add @babel/core@7.4.5 @babel/preset-env@7.4.5 --dev`

- `@babel/core` 核心包
- `@babel/preset-env` 用来替换转换
- `@7.4.5` 最经典的版本

#### Babel 基本配置

项目根目录新建`.babelrc`文件，`babel`转换器配置就写在这个文件里面

```
{
    "presets":[
        [
                "@babel/preset-env",{
                "targets":{
                    "node":"current"
                }
            }
        ]
    ]
}
```

#### 转换原因

Jest 里面有一个`babel-jest`组件，使用`yarn jest`的时候，

1. 先去检查开发环境中是否安装了`babel`，也就是查看有没有`babel-core`
2. 有`babel-core`，再去查看`.babelrc`配置文件，根据配置文件进行转换

#### 异步代码测试

1. 回调函数式

**问题** 这样写是有问题的，因为方法还没有回调，结果已经完成了，通过是仅代表方法可用，不代表结果与期待值相等，不能保证结果是正确的

```
import { fetchData } from './fetchData.js'

test('fetchData 测试',()=>{
   fetchData((data)=>{
       expect(data).toEqual({
           success: true
       })

   })
  })

```

**解决** 必须加入一个`done`方法，保证回调已经完成，这时候才表示测试成功

```
import { fetchData } from './fetchData.js'

test('fetchData 测试',(done)=>{
   fetchData((data)=>{
       expect(data).toEqual({
           success: true
       })
       done()
   })
  })
```

2. Promise 类

**注意** 需要使用`return`才能测试成功

```
test('FetchTwoData 测试', ()=>{
       return  fetchTwoData().then((response)=>{
            expect(response.data).toEqual({
                success: true
            })
        })
  })
```

3. 不存在接口的测试方法

**注意** 请求不存在的接口，我们使用`catch`来捕获异常

但这样是错误的，比如现在我们把异步请求代码改正确后，我们再走一下测试，还是可以通过测试的。

因为测试用例使用了`catch`方法，也就是说只有出现异常的时候才会走这个方法，而现在没有出现异常，就不会走这个测试方法，Jest 就默认这个用例通过了测试。

```
test('FetchThreeData 测试', ()=>{
      return fetchThreeData().catch((e)=>{
        expect(e.toString().indexOf('404')> -1).toBe(true)
      })
  })
```

**解决** 只要使用`expect.assertions(1)`就可以了，意思是"断言，必须执行一次`expect`方法才可以通过测试"

这时候测试用例就无法正常通过测试了，因为此时我们的地址是存在并正确返回结果的。我们需要改成错误的地址，才能通过测试。

```
test('FetchThreeData 测试', ()=>{
      /**断言，必须执行一次expect*/
      expect.assertions(1)
      return fetchThreeData().catch((e)=>{
        expect(e.toString().indexOf('404')> -1).toBe(true)

      })
  })
```

4. async / await

   - `resolve` 用于把现有对象转换成`Promise`对象
   - `toMatchObject` 进行匹配对象中的属性

```
test('FetchFourData 测试', async()=>{
        //resolves把现有对象转换成Promise对象，
        //toMatchObject 匹配对象中的属性
        await expect(fetchFourData()).resolves.toMatchObject({
            data:{
                success:true
            }
        })
})
```

简化代码

```
test('FetchFourData 测试', async()=>{
        const response  = await fetchFourData()
        expect(response.data).toEqual({
            success : true
        })
})
```

#### Jest 中的四个钩子函数

#### Jest 中对测试用例进行分组

#### 钩子函数作用域
