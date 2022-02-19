## Callouts

<Callout type="info">
  This is an **info callout**
</Callout>
  
<Callout type="tip">
  This is a **tip callout**
</Callout>

<Callout type="success">
  This is a **success callout**
</Callout>

<Callout type="warning">
  This is a **success callout**
</Callout>

<Callout type="danger">
  This is a **danger callout**
  <Tooltip content="Hi there, nice to meet you">
    Hover me
  </Tooltip>
</Callout>

## Tooltips

<Tooltip content="Hi there, nice to meet you">Hover me</Tooltip> to show tooltips <Icons.CheckCircle className="inline-block" /> in docs.

## Accordion

<Accordion
  values={[
     {title: "Click me", content: "And **I** `will` be visible"},
     {title: "Is this free", content: "Yes! everything is absolutely free"},
     {title: "Hello world", content: "World hello"},
     {title: "How react inside markdown?", content: "Thanks to MDX"},
]}           
/>

## Images

![image](https://user-images.githubusercontent.com/85922663/154807596-88e526dd-46d0-439d-8a5e-0464e09f3e2a.png)

## Sandpack

<Sandpack
  template="react"
  files={{
    "/App.js": `import Rm from 'react-markdown'
import {Tooltip} from 'react-tiny-tooltip'
export default function App() {
  return (
    <div>
          <Rm>Hello *world*. **Wassup**</Rm>
          <Tooltip content="Hey there">Hover me 🙌</Tooltip>
    </div>
  )
}`,
  }}
  customSetup={{
    dependencies: {
      react: "17.0.2",
      "react-dom": "17.0.2",
      "react-scripts": "4.0.0",
      "react-markdown": "8.0.0",
      "react-tiny-tooltip": "*"
    },
  }}
/>

## Valid jsx?

<button onClick={() => alert('button clicked!')}>Click me!</button>

  <span
    style={{
      backgroundColor: '#73e9c1',
      borderRadius: '20px',
      color: '#fff',
      padding: '10px',
      cursor: 'pointer',
    }}
    className="not-prose"
    onClick={() => {
      alert(`You clicked me!`)
    }}>
    Hello from a custom component. Btw, click me!
  </span>
