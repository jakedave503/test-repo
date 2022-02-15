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
     {title: "Click me", content: "And I will be visible"},
     {title: "Is this free", content: "Yes! everything is absolutely free"},
     {title: "Hello world", content: "World hello"},
     {title: "How react inside markdown?", content: "Thanks to MDX"},
]}           
/>

## Embeds

<Embed url="https://tally.so/embed/w4x9Bw?alignLeft=1&hideTitle=1&transparentBackground=1" />

<iframe
  src="https://tally.so/embed/w4x9Bw?alignLeft=1&hideTitle=1&transparentBackground=1"
  width="100%"
  height="500"
  frameborder="0"
  marginheight="0"
  marginwidth="0"
  title="Request for Integration">
</iframe>


Regular `iframe` tag
<iframe src="https://tally.so/embed/w4x9Bw?alignLeft=1&hideTitle=1&transparentBackground=1" />

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
