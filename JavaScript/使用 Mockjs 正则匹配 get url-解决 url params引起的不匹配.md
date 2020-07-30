# 使用 Mockjs 正则匹配 get url -- 解决 url params 引起的不匹配

问题描述

以下两个 Mockjs 用于拦截业务请求。

```js
Mock.mock('//dev.project.com/gateway/xxx-server/api/question/page/query', {
  code: '2000',
  data: '',
  message: 'mock',
  success: true
});

Mock.mock('//dev.project.com/gateway/auth/api/b/login', {
  code: '2000',
  data: 'token',
  message: 'mock',
  success: true
});
```

利用 axiox 的 HTTP.ts

```js
private getConfig(config?: AxiosRequestConfig): AxiosRequestConfig {
    return Object.assign({}, this.config, config || {});
  }
  protected async get(url: string, config?: AxiosRequestConfig) {
    try {
      const res: IResponse<any> = await axios.get(url, this.getConfig(config));
      return res;
    } catch (e) {
      console.log(e);
    }
    return {
      success: false,
      data: null
    };
  }
  protected async post(url: string, data?: any, config?: AxiosRequestConfig) {
    try {
      const res: IResponse<any> = await axios.post(
        url,
        data,
        this.getConfig(config)
      );
      return res;
    } catch (e) {
      console.log(e);
    }
    return {
      success: false,
      data: null
    };
  }
```


发送访问请求：

> Request URL: http://dev.project.hrtps.com/gateway/servier-server/api/question/page/query?pageNo=1&pageSize=10&businessType=BUSINESS_PLAN&questionType=TUTOR

#### 没有匹配 Mockjs 的原因是 Mock.mock(url, ...) 字符型 url 会做全量匹配，url 后面带的参数也会参与匹配。


Mockjs 支持正则方式 url。

修改 Mockjs
```js
// Mock.mock('//dev.project.com/gateway/xxx-server/api/question/page/query', {
//
Mock.mock(/\/\/dev\.project\.hrtps\.com\/gateway\/servier-server\/api\/question\/page\/query[\s|\S]*/, {
  code: '2000',
  data: '',
  message: 'mock',
  success: true
});
```

Tips:
>
> \s = 空白字符
> 
> \S = 非空白字符
> 
> x|y = x或y
> 
> [xyz] = 字符集和
> 
> * = 任意匹配
>
> [\s|\S]* = 任意字符匹配任意次
> 
 
[MDN 正则](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

