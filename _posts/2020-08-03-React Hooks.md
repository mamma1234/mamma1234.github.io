---
layout: post
title: "React Hooks"
description: 
headline: 
modified: 2020-08-31
category: webdevelopment
imagefeature: cover3.jpg
tags: [React Hooks]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# React Hooks
useInput
useTabs
useTitle
usePageLeave
useClick
useFadeIn
useFullscreen
useHover
useNetwork
useNotification
useScroll
usePreventLeave
useConfirm
useAxios

## useInput 

```JavaScript
const useInput = initialValue => {
  const [value, setValue] = useState(initialValue);
  const onChange = event => {
    const {
      target: { value }
    } = event;
    // console.log(event.target);
    // console.log(event.target.value);
    setValue(value);
  };
  return { value, onChange };
};

const useInput2 = (initialValue, validator) => {
  const [value, setValue] = useState(initialValue);
  const onChange = event => {
    const {
      target: { value }
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(value);
    }
    if (willUpdate) {
      setValue(value);
    }
  };

  return { value, onChange };
};



export default function Hook1() {
  const [item, setItem] = useState(1);
  const incrementItem = () => setItem(item + 1);
  const decrementItem = () => setItem(item - 1);
  const name = useInput("Mr:");
  const maxLen = value => value.length < 10;
  const name2 = useInput2("Mr:", maxLen);
  return (
    <div className="App">
      <h1>Hello State Hook {item}</h1>
      <button onClick={incrementItem}>Increment</button>
      <button onClick={decrementItem}>Decrement</button>
      <input placeholder="Name" {...name} />
      <input placeholder="Name" {...name2} />
    </div>
  );
}
```


## useTabs 


```JavaScript

const content = [
  {
    tab: "Section 1",
    content: "i'm the content of the Section 1"
  },
  {
    tab: "Section 2",
    content: "I'm the content of the Section 2"
  }
];

const useTabs = (initialTab, allTabs) => {
  console.log("initialTab", initialTab, "allTabs", allTabs);
  if (!allTabs || !Array.isArray(allTabs)) {
    return;
  }
  const [currentIndex, setCurrentIndex] = useState(initialTab);
  console.log(currentIndex, allTabs[0]);
  return {
    currentItem: allTabs[currentIndex],
    changeItem: setCurrentIndex
  };
};




export default function Hook1() {
  const [item, setItem] = useState(1);
  // const tabs = useTabs(0, content);
  const { currentItem, changeItem } = useTabs(0, content);
  console.log(currentItem);
  return (
    <div className="App">
      <h1>Hello State Hook {item}</h1>
      {content.map((section, index) => (
        <button onClick={() => changeItem(index)}>{section.tab}</button>
      ))}
      <div>{currentItem.content}</div>
    </div>
  );
}

```