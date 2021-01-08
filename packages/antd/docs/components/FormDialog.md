# FormDialog

> 弹窗表单，主要用在简单的事件打开表单场景

## Markup Schema 案例

```tsx
import React from 'react'
import { FormDialog, FormItem, Input } from '@formily/antd'
import { Field, useForm } from '@formily/react'
import { createSchemaField } from '@formily/react-schema-field'
import { Button, Form } from 'antd'

const SchemaField = createSchemaField({
  components: {
    FormItem,
    Input,
  },
})

export default () => {
  return (
    <Button
      onClick={() => {
        FormDialog('弹窗表单', () => {
          return (
            <Form labelCol={{ span: 6 }} wrapperCol={{ span: 14 }}>
              <SchemaField>
                <SchemaField.String
                  name="aaa"
                  required
                  title="输入框1"
                  x-decorator="FormItem"
                  x-component="Input"
                />
                <SchemaField.String
                  name="bbb"
                  required
                  title="输入框2"
                  x-decorator="FormItem"
                  x-component="Input"
                />
                <SchemaField.String
                  name="ccc"
                  required
                  title="输入框3"
                  x-decorator="FormItem"
                  x-component="Input"
                />
                <SchemaField.String
                  name="ddd"
                  required
                  title="输入框4"
                  x-decorator="FormItem"
                  x-component="Input"
                />
              </SchemaField>
              <FormDialog.Footer>
                <span style={{ marginLeft: 4 }}>扩展文案</span>
              </FormDialog.Footer>
            </Form>
          )
        })
          .open({
            initialValues: {
              aaa: '123',
            },
          })
          .then(console.log)
      }}
    >
      点我打开表单
    </Button>
  )
}
```

## JSON Schema 案例

```tsx
import React from 'react'
import { FormDialog, FormItem, Input } from '@formily/antd'
import { Field, useForm } from '@formily/react'
import { createSchemaField } from '@formily/react-schema-field'
import { Button, Form } from 'antd'

const SchemaField = createSchemaField({
  components: {
    FormItem,
    Input,
  },
})

const schema = {
  type: 'object',
  properties: {
    aaa: {
      type: 'string',
      title: '输入框1',
      required: true,
      'x-decorator': 'FormItem',
      'x-component': 'Input',
    },
    bbb: {
      type: 'string',
      title: '输入框2',
      required: true,
      'x-decorator': 'FormItem',
      'x-component': 'Input',
    },
    ccc: {
      type: 'string',
      title: '输入框3',
      required: true,
      'x-decorator': 'FormItem',
      'x-component': 'Input',
    },
    ddd: {
      type: 'string',
      title: '输入框4',
      required: true,
      'x-decorator': 'FormItem',
      'x-component': 'Input',
    },
  },
}

export default () => {
  return (
    <Button
      onClick={() => {
        FormDialog('弹窗表单', () => {
          return (
            <Form labelCol={{ span: 6 }} wrapperCol={{ span: 14 }}>
              <SchemaField schema={schema} />
              <FormDialog.Footer>
                <span style={{ marginLeft: 4 }}>扩展文案</span>
              </FormDialog.Footer>
            </Form>
          )
        })
          .open({
            initialValues: {
              aaa: '123',
            },
          })
          .then(console.log)
      }}
    >
      点我打开表单
    </Button>
  )
}
```

## 纯 JSX 案例

```tsx
import React from 'react'
import { FormDialog, FormItem, Input, DialogFooter } from '@formily/antd'
import { Field, useForm } from '@formily/react'
import { Button, Form } from 'antd'

export default () => {
  return (
    <Button
      onClick={() => {
        FormDialog('弹窗表单', () => {
          return (
            <Form labelCol={{ span: 6 }} wrapperCol={{ span: 14 }}>
              <Field
                name="aaa"
                required
                title="输入框1"
                decorator={[FormItem]}
                component={[Input]}
              />
              <Field
                name="bbb"
                required
                title="输入框2"
                decorator={[FormItem]}
                component={[Input]}
              />
              <Field
                name="ccc"
                required
                title="输入框3"
                decorator={[FormItem]}
                component={[Input]}
              />
              <Field
                name="ddd"
                required
                title="输入框4"
                decorator={[FormItem]}
                component={[Input]}
              />
              <FormDialog.Footer>
                <span style={{ marginLeft: 4 }}>扩展文案</span>
              </FormDialog.Footer>
            </Form>
          )
        })
          .open({
            initialValues: {
              aaa: '123',
            },
          })
          .then(console.log)
      }}
    >
      点我打开表单
    </Button>
  )
}
```

## API

### FormDialog

```ts pure
type FormDialogHandler = {
  //打开弹窗，接收表单属性，可以传入initialValues/values/effects etc.
  open(props: Formily.Core.Types.IFormProps): Promise<any> //返回表单数据
  //关闭弹窗
  close(): void
}

interface IFormDialog {
  (
    title: React.ReactNode, //如果是ReactNode，则作为弹窗title传入
    renderer: (resolve: () => void, reject: () => void) => React.ReactElement
  ): FormDialogHandler
  (
    title: ModalProps, //如果是对象，则作为ModalProps传入
    renderer: (resolve: () => void, reject: () => void) => React.ReactElement
  ): FormDialogHandler
}
```

### FormDialog.Footer

无属性，只接收子节点