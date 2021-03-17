---
layout: post
title: "React"
description: 
headline: 
modified: 2021-02-23
category: webdevelopment
imagefeature: cover3.jpg
tags: [React External JavaScript]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 4 Ways to Add External JavaScript Files in React

## React-script-tag

```JavaScript
  import ScriptTag from 'react-script-tag';
  const Demo = props => (
  <ScriptTag type="text/javascript" src="/path/to/resource.js" />
  )
```

## React Helmet

```JavaScript
  import {Helmet} from "react-helmet";
  const Demo = props => (
  <div className="application">
              <Helmet>
                <script src="/path/to/resource.js" type="text/javascript" />
              </Helmet>
              ...
          </div>
    
  );
```

## DOM Method

```JavaScript
  export const appendScript = (scriptToAppend) => {
      const script = document.createElement("script");
      script.src = scriptToAppend;
      script.async = true;
      document.body.appendChild(script);
  }

  export const removeScript = (scriptToremove) => {
      let allsuspects=document.getElementsByTagName("script");
      for (let i=allsuspects.length; i>=0; i--){
  if (allsuspects[i] && allsuspects[i].getAttribute("src")!==null 
    && allsuspects[i].getAttribute("src").indexOf(`${scriptToremove}`)                !== -1 ){
            allsuspects[i].parentNode.removeChild(allsuspects[i])
          }    
      }
  }

  import {appendScript} from 'utils/appendScript'
  import {removeScript} from 'utils/removeScript'
  class Demo extends React.Component {
  componentDidMount () {
      appendScript("/path/to/resource.js");
  }
  componentDidUnmount () {
      removeScript("/path/to/resource.js")
  }
  ...
  }
```

## React Hooks

```JavaScript
  import { useEffect } from 'react';
  const importScript = resourceUrl=> {
    useEffect(() => {
      const script = document.createElement('script');
      script.src = resourceUrl;
      script.async = true;
      document.body.appendChild(script);
  return () => {
        document.body.removeChild(script);
      }
    }, [resourceUrl]);
  };
  export default importScript;
```