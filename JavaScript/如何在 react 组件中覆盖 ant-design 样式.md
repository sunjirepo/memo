# 如何在 react 组件中覆盖 ant-design 样式.md

说明：

复用 antd 的组件，仅样式上微调。

利用 scss 的 :global 属性能够覆盖原 ant-design 的样式。

将其（:global）包裹在另一个 scss 中控制修改样式的范围仅限于某一组件，不污染其他 ant-design。

示例：

antd Tabs 组件，微调 Tab 居中，且 Tab 的长度占满总长。

组件代码: 

```js
import React from 'react';
import { Tabs } from 'antd';
import styles from './Coach.module.scss';

const { TabPane } = Tabs;

const Coach: React.FunctionComponent = props => {
  return (
    <div className={styles.main}>
      <div className={styles.title}>辅导报告</div>
      <Tabs
        defaultActiveKey="1"
        centered
        className={styles.tabs}
      >
        <TabPane tab="员工答题汇总" key="1">
          <div>员工答题汇总</div>
        </TabPane>
        <TabPane tab="PK赛设置" key="2">
          <div>PK赛设置</div>
        </TabPane>
      </Tabs>
    </div>
  );
}
export default Coach;

```

对应 css 组件 -- Coach.module.scss: 

```css
.main {
  padding: 24px 26px 0px 24px;
}
.title {
  width:108px;
  height:28px;
  font-size:18px;
  font-family:PingFangSC-Medium,PingFang SC;
  font-weight:500;
  color:rgba(115,160,250,1);
  line-height:28px;
}
.tabs {
  padding-top: 0px;
}
.tabs {
  :global {
    .ant-tabs-nav-list{
      position: relative;
      display: flex;
      width: 100%;
    }
  }

  :global {
    .ant-tabs-tab {
      position: relative;
      display: inline-flex;
      align-items: center;
      margin: 0 32px 0 0;
      padding: 12px 0;
      font-size: 14px;
      background: transparent;
      border: 0;
      outline: none;
      cursor: pointer;
      width: 50%;
      justify-content: center;
    }
  }
}
```

待完善，+ Codepan 代码样例。