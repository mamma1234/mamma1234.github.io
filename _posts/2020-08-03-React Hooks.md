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
useClick
useHover
useConfirm
usePreventLeave


usePageLeave
useFadeIn
useFullscreen
useNetwork
useNotification
useScroll


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


## useTitle

```JavaScript

const useTitle = initialTitle => {
  const [title, setTitle] = useState(initialTitle);
  const updateTitle = () => {
    const htmlTitle = document.querySelector("title");
    htmlTitle.innerText = title;
  };
  useEffect(updateTitle, [title]);
  return setTitle;
};



export default function Hook2() {
  const [item, setItem] = useState(2);
  const sayHello = () => console.log("hello");

  // useEffect(() => {
  //   sayHello();
  // });
  const [number, setNumber] = useState(0);
  const [aNumber, setAnumber] = useState(0);
  useEffect(sayHello, []);

  const titleUpdater = useTitle("Loading...");
  setTimeout(() => titleUpdater("Home"), 5000);

  return (
    <div className="App">
      <h1>Hello Effect Hook {item}</h1>
      <button onClick={() => setNumber(number + 1)}>{number}</button>
      <button onClick={() => setAnumber(aNumber + 1)}>{aNumber}</button>
    </div>
  );
}

```

## useClick & useHover

```JavaScript

const useClick = onClick => {
  if (typeof onClick !== "function") {
    return;
  }
  const element = useRef();
  useEffect(() => {
    if (element.current) {
      element.current.addEventListener("click", onClick);
    //   element.current.addEventListener("mouseenter", onClick); //useHover
    }
    return () => {
      if (element.current) {
        console.log("remove event");
        element.current.removeEventListener("click", onClick);
        // element.current.removeEventListener("mouseenter", onClick); //useHover
      }
    };
  }, []);
  return element;
};



export default function Hook2() {
  const [item, setItem] = useState(2);
  const sayHello = () => console.log("hello");


  const potato = useRef();
  setTimeout(() => potato.current.focus(), 5000);

  // const sayHello = () => console.log("say hello");
  const title = useClick(sayHello);
  return (
    <div className="App">
      <h1>Hello Effect Hook {item}</h1>
      <input ref={potato} placeholder="la" />
      <h1 ref={title}>Hi</h1>
    </div>
  );
}

```


## useConfirm


## usePreventLeave
