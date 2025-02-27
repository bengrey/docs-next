# Свойства экземпляра

## $data

- **Тип:** `Object`

- **Подробности:**

  Объект с данными, за которыми осуществляет наблюдение экземпляр компонента. Экземпляр компонента проксирует доступ к свойствам объекта данных.

- **См. также:** [Options API / Локальное состояние — data](options-data.md#data)

## $props

- **Тип:** `Object`

- **Подробности:**

  Объект, содержащий текущие входные параметры, которые получил компонент. Экземпляр компонента проксирует доступ к свойствам объекта входных параметров.

## $el

- **Тип:** `any`

- **Только для чтения**

- **Подробности:**

  Корневой элемент DOM, которым управляет экземпляр компонента.

  Для компонентов использующих [фрагменты](../guide/migration/fragments.md), `$el` будет узлом DOM, с помощью которого Vue будет отслеживать место компонента в DOM. Рекомендуется использовать [ссылки на элементы шаблона](../guide/component-template-refs.md) для доступа к элементам DOM напрямую, а не полагаться на `$el`.

## $options

- **Тип:** `Object`

- **Только для чтения**

- **Подробности:**

  Опции инициализации, используемые для текущего экземпляра компонента. Полезно, если потребуется добавить пользовательские свойства в опции:

  ```js
  const app = createApp({
    customOption: 'foo',
    created() {
      console.log(this.$options.customOption) // => 'foo'
    }
  })
  ```

## $parent

- **Тип:** `Экземпляр компонента`

- **Только для чтения**

- **Подробности:**

  Родительский экземпляр, если таковой имеется.

## $root

- **Тип:** `Экземпляр компонента`

- **Только для чтения**

- **Подробности:**

  Экземпляр корневого компонента текущего дерева компонентов. Если у текущего экземпляра нет родителя, то значением будет он сам.

## $slots

- **Тип:** `{ [name: string]: (...args: any[]) => Array<VNode> | undefined }`

- **Только для чтения**

- **Подробности:**

  Используется для программного доступа к содержимому, [распределяемому с помощью слотов](../guide/component-basics.md#распределение-контента-слотами). Каждый [именованный слот](../guide/component-slots.md#именованные-слоты) имеет соответствующее свойство (например, содержимое `v-slot:foo` будет доступно через `this.$slots.foo()`). В свойстве `default` будут либо узлы, не попавшие в какой-либо именованный слот, либо содержимое `v-slot:default`.

  Доступ к `this.$slots` пригодится при создании компонента с помощью [render-функции](../guide/render-function.md).

- **Пример:**

  ```html
  <blog-post>
    <template v-slot:header>
      <h1>Обо мне</h1>
    </template>

    <template v-slot:default>
      <p>
        Какое-то содержимое страницы, которое будет доступно в $slots.default.
      </p>
    </template>

    <template v-slot:footer>
      <p>Copyright 2021 Evan You</p>
    </template>
  </blog-post>
  ```

  ```js
  const app = createApp({})

  app.component('blog-post', {
    render() {
      return h('div', [
        h('header', this.$slots.header()),
        h('main', this.$slots.default()),
        h('footer', this.$slots.footer())
      ])
    }
  })
  ```

- **См. также:**
  - [Встроенный компонент `<slot>`](built-in-components.md#slot)
  - [Распределение контента слотами](../guide/component-basics.md#распределение-контента-слотами)
  - [Render-функции — Слоты](../guide/render-function.md#слоты)

## $refs

- **Тип:** `Object`

- **Только для чтения**

- **Подробности:**

  Объект из DOM-элементов и экземпляров компонентов, зарегистрированных с помощью [атрибутов `ref`](../guide/component-template-refs.md).

- **См. также:**
  - [Ссылки на элементы шаблона](../guide/component-template-refs.md)
  - [Специальные атрибуты — ref](special-attributes.md#ref)

## $attrs

- **Тип:** `Object`

- **Только для чтения**

- **Подробности:**

  Содержит привязки атрибутов и события в родительском компоненте, которые не были распознаны (и исключены) как [входные параметры](options-data.md#props) компонента или [пользовательские события](options-data.md#emits). Если компонент не объявляет входные параметры или пользовательские события, тут будут все привязки из родительского компонента, которые можно передать через `v-bind="$attrs"` внутреннему компоненту  — удобно при создании компонентов высшего порядка (HOC, High Order Components).

- **См. также:**
  - [Передача обычных атрибутов](../guide/component-attrs.md)
  - [Options API / Разное — inheritAttrs](./options-misc.md#inheritattrs)
