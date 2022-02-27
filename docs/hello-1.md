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
  title="Hi there">
  Hello world 👋
</Accordion>

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

## Grids

<Grid
  features={[
    {title: "Introduction", description: "Get started with Hyperdocs and build your first docs site", color: "blue"},
    {title: "Quickstart", description: "Create your first documentation site in less than a minute", color: "green"},
    {title: "How it works", description: "How Hyperdocs works behind the scenes", color: "teal"},
    {title: "Migration guide", description: "Move your docs site to Hyperdocs and simplify your docs setup", color: "gray"}
  ]}
/>
