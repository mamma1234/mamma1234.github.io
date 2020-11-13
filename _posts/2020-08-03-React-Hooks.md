---
layout: post
title: "React Hooks"
description: 
headline: 
modified: 2020-08-03
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

- 기본 Hook
  - useState
  - useEffect
  - useContext

- 추가 Hooks
  - useReducer
  - useCallback
  - useMemo
  - useRef
  - useImperativeHandle
  - useLayoutEffect
  - useDebugValue

### useState
```JavaScript
import React, { useState } from "react";

const UseStateSample = () => {
  const [value, setValue] = useState(0);
  return (
    <div>
      <p>
        UseState : 현재 카운터 값은 <b>{value}</b> 입니다.
      </p>
      <button onClick={() => setValue(value + 1)}>+1</button>
      <button onClick={() => setValue(value - 1)}>-1</button>
    </div>
  );
};

export default UseStateSample;
```

### useEffect
```JavaScript
import React, { useState, useEffect } from "react";

const UseEffectSample = (pros) => {
  const [name, setName] = useState("");
  const [nickname, setNickname] = useState("");
  const [parentname, setParentname] = useState(pros.parentname);

  useEffect(() => {
    console.log("렌더링 될 때마다 수행");
    console.log({
      name,
      nickname
    });
  });

  useEffect(() => {
    console.log("마운트 될 때만 실행됩니다.");
  }, []);

  useEffect(() => {
    console.log("name stats가 변환될때만 수행 ", name);
  }, [name]);

  useEffect(() => {
    console.log("effect");
    console.log(name);
    return () => {
      console.log("cleanup");
      console.log(name);
    };
  });

  useEffect(() => {
    return () => {
      console.log("언마운트 될 때만 실행됩니다.");
    };
  }, []);

  const onChangeName = (e) => {
    setName(e.target.value);
  };

  const onChangeNickname = (e) => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        UseEffect:
        <input value={name} onChange={onChangeName} />
        <input value={nickname} onChange={onChangeNickname} />
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임: </b>
          {nickname}
        </div>
        <div>
          <button onClick={() => setParentname(pros.parentname)}>
            {" "}
            부모이름가져오기
          </button>
          <b>부모이름: </b>
          {parentname}
        </div>
      </div>
    </div>
  );
};

export default UseEffectSample;

```

### useContext

```JavaScript
import React, { useState } from "react";

const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

const ThemeContext = React.createContext(themes.light);

function UseContextSample() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = React.useContext(ThemeContext);
  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );
}

export default UseContextSample;

```

#### Composition 합성

```JavaScript
import React, { useState } from "react";

function FancyBorder(props) {
  return (
    <div className={"FancyBorder FancyBorder-" + props.color}>
      {props.children}
    </div>
  );
}

function Composition() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">합성 Composition</h1>
      <p className="Dialog-message">Thank you for visiting our spacecraft!</p>
    </FancyBorder>
  );
}

export default Composition;
```


### useReducer
```JavaScript

- 예시 1
import React, { useReducer } from "react";

function reducer(state, action) {
  // action.type 에 따라 다른 작업 수행
  switch (action.type) {
    case "INCREMENT":
      return { value: state.value + 1 };
    case "DECREMENT":
      return { value: state.value - 1 };
    default:
      // 아무것도 해당되지 않을 때 기존 상태 반환
      return state;
  }
}

const UseReducerSample = () => {
  const [state, dispatch] = useReducer(reducer, { value: 0 });

  return (
    <div>
      <h4>useReducer</h4>
      <p>
        현재 카운터 값은 <b>{state.value}</b> 입니다.
      </p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+1</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-1</button>
    </div>
  );
};

export default UseReducerSample;



- 예시 2
import React, { useReducer } from 'react';

function reducer(state, action) {
  return {
    ...state,
    [action.name]: action.value
  };
}

const UseReducer2Sample = () => {
  const [state, dispatch] = useReducer(reducer, {
    name: '',
    nickname: ''
  });
  const { name, nickname } = state;
  const onChange = e => {
    dispatch(e.target);
  };

  return (
    <div>
      <div>
        <input name="name" value={name} onChange={onChange} />
        <input name="nickname" value={nickname} onChange={onChange} />
      </div>
      <div>
        <div>
          <b>이름:</b> {name}
        </div>
        <div>
          <b>닉네임: </b>
          {nickname}
        </div>
      </div>
    </div>
  );
};

export default UseReducer2Sample;

```
### useCallback
```JavaScript

import React, { useState, useMemo, useCallback } from "react";

const getAverage = (numbers) => {
  console.log("평균값 계산중..");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const UseCallbackSample = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = useCallback((e) => {
    console.log("onChange 함수");
    setNumber(e.target.value);
  }, []); // 컴포넌트가 처음 렌더링 될 때만 함수 생성
  const onInsert = useCallback(
    (e) => {
      console.log("onInsert 함수");
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber("");
    },
    [number, list]
  ); // number 혹은 list 가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <h4>useCallback</h4>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
};

export default UseCallbackSample;


```
### useMemo
```JavaScript

import React, { useState, useMemo } from "react";

const getAverage = (numbers) => {
  console.log("평균값 ? 계산중..");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};
const getAverage2 = (numbers) => {
  console.log("평균값 O 계산중..");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const UseMemoSample = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = (e) => {
    console.log("onChange 함수");
    setNumber(e.target.value);
  };
  const onInsert = (e) => {
    console.log("onInsert 함수");
    const nextList = list.concat(parseInt(number));
    setList(nextList);
    setNumber("");
  };

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <h4>useMemo</h4>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <p>
          <b>평균 값(useMemo):</b> {avg}
        </p>
        <p>
          <b>평균 값(렌더링 될때 마다 실행):</b> {getAverage2(list)}
        </p>
      </div>
    </div>
  );
};

export default UseMemoSample;


```
### useRef
```JavaScript
import React, { useState, useMemo, useRef, useCallback } from "react";

const getAverage = (numbers) => {
  console.log("평균값 계산중..");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const UseRefSample = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");
  const inputEl = useRef(null);

  const onChange = useCallback((e) => {
    setNumber(e.target.value);
  }, []); // 컴포넌트가 처음 렌더링 될 때만 함수 생성
  const onInsert = useCallback(
    (e) => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber("");
      inputEl.current.focus();
    },
    [number, list]
  ); // number 혹은 list 가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <h4>useRef</h4>
      <input value={number} onChange={onChange} ref={inputEl} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균 값:</b> {avg}
      </div>
    </div>
  );
};

export default UseRefSample;

```

#### ref
```JavaScript
import React, { Component } from "react";

class RefSample extends Component {
  state = {
    height: 0
  };

  input = null;
  box = null;

  handleClick = () => {
    this.input.focus();
  };

  componentDidMount() {
    this.setState({
      height: this.box.clientHeight
    });
  }

  render() {
    return (
      <div>
        <input
          id="a"
          ref={(ref) => {
            console.log(ref);
            this.input = ref;
          }}
        />
        <button onClick={this.handleClick}>Focus Input</button>
        <div
          ref={(ref) => {
            this.box = ref;
          }}
        >
          <h2>TITLE</h2>
          <p>Content</p>
        </div>
        <p>
          <b>height:</b> {this.state.height}
        </p>
      </div>
    );
  }
}

export default RefSample;

```


### useImperativeHandle
```JavaScript
```
### useLayoutEffect
```JavaScript
```
### useDebugValue
```JavaScript
```



# User Hook
- useInput
- useTabs
- useTitle
- useClick
- useHover
- useConfirm
- usePreventLeave
- useBeforeLeave
- useFadeIn
- useNetwork
- useFullscreen
- useScroll
- useNotification
- useAxios

### useInput 

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


### useTabs 

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


### useTitle

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

### useClick & useHover

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


### useConfirm && usePreventLeave

```JavaScript

import React, { useState, useEffect, useRef } from "react";
import "./styles.css";

const useConfirm = (message = "", onConfirm, onCancel) => {
  if (!onConfirm && typeof onConfirm !== "function") {
    return;
  }

  if (onCancel && typeof onCancel !== "function") {
    return;
  }

  const confirmAction = () => {
    if (confirm(message)) {
      onConfirm();
    } else {
      onCancel();
    }
  };
  return confirmAction;
};

const usePreventLeave = () => {
  const listener = (event) => {
    event.preventDefault();
    event.returnValue = "";
  };
  const enablePrevent = () => window.addEventListener("beforeunload", listener);
  const disablePrevent = () =>
    window.removeEventListener("beforeunload", listener);
  return { enablePrevent, disablePrevent };
};

export default function Hook3() {
  const [item, setItem] = useState(3);
  const deleteWorld = () => console.log("Delete the world");
  const abort = () => console.log("Aborted");
  const confirmDelete = useConfirm("are you sure", deleteWorld, abort);

  const { enablePrevent, disablePrevent } = usePreventLeave();
  return (
    <div className="App">
      <h1>Hello Effect Hook {item}</h1>
      <button onClick={confirmDelete}>Delete the world</button>
      <button onClick={enablePrevent}>protect</button>
      <button onClick={disablePrevent}>unprotect</button>
    </div>
  );
}

```


### useBeforeLeave

```JavaScript

import React, { useState, useEffect, useRef } from "react";
import "./styles.css";

const useBeforeLeave = (onBefore) => {
  if (!onBefore && typeof onBefore !== "function") {
    return;
  }

  const handle = (event) => {
    console.log("leave");
    const { clientY } = event;
    if (clientY <= 0) {
      onBefore();
    }
  };

  useEffect(() => {
    document.addEventListener("mouseleave", handle);
    return () => document.removeEventListener("mouseleave", handle);
  }, []);
};

export default function Hook4() {
  const [item, setItem] = useState(4);
  const beforeLife = () => console.log("pls don't leave");
  useBeforeLeave(beforeLife);

  return (
    <div className="App">
      <h1>Hello Effect Hook {item}</h1>
    </div>
  );
}

```


### useFadeIn

```JavaScript
import React, { useState, useEffect, useRef } from "react";
import "./styles.css";

const useFadeIn = (duration = 1, delay = 0) => {
  if (typeof duration != "number" || typeof delay != "number") {
    return;
  }
  const element = useRef();
  // console.log("element.current", element.current);
  useEffect(() => {
    if (element.current) {
      const { current } = element;
      console.log("opacity");
      current.style.transition = `opacity ${duration}s ease-in-out ${delay}s`;
      current.style.opacity = 1;
    }
  }, []);
  return { ref: element, style: { opacity: 0 } };
};
export default function Hook5() {
  // const [item, setItem] = useState(5);
  const fadeInH1 = useFadeIn(1, 2);
  const fadeInP = useFadeIn(5, 10);
  return (
    <div className="App">
      <h1 {...fadeInH1}>Hello Ref Hook</h1>
      <p {...fadeInP}>lorem ipsum adsaf</p>
    </div>
  );
}

```






### useNetwork

```JavaScript


import React, { useState, useEffect, useRef } from "react";
import "./styles.css";

const useNetwork = (onChange) => {
  const [status, setStatus] = useState(navigator.onLine);
  const handleChange = () => {
    if (typeof onChange === "function") {
      onChange(navigator.onLine);
    }
    setStatus(navigator.onLine);
  };
  useEffect(() => {
    window.addEventListener("online", handleChange);
    window.addEventListener("offline", handleChange);
    () => {
      window.removeEventListener("online", handleChange);
      window.removeEventListener("offline", handleChange);
    };
  }, []);
  return status;
};

export default function Hook5() {
  // const [item, setItem] = useState(5);
  const handleNetworkChange = (online) => {
    console.log(online ? "web online" : "we offine");
  };
  const onLine = useNetwork(handleNetworkChange);
  return (
    <div className="App">
      <h1>Hello Ref Hook {onLine ? "onLine" : "offline"} </h1>
    </div>
  );
}


```




### useScroll

```JavaScript



import React, { useState, useEffect, useRef } from "react";
import "./styles.css";

const useScroll = () => {
  const [state, setState] = useState({ x: 0, y: 0 });
  const onScroll = (evnet) => {
    console.log("y", window.scrollY, " x", window.scrollX);
    setState({ y: window.scrollY, x: window.scrollX });
  };
  useEffect(() => {
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  });
  return state;
};

export default function Hook6() {
  // const [item, setItem] = useState(5);
  const { y } = useScroll();
  console.log("y", y);
  return (
    <div className="App" style={{ height: "1000vh" }}>
      <h1 style={{ position: "fixed", color: y > 100 ? "red" : "blue" }}>
        Hi Scroll
      </h1>
    </div>
  );
}


```








### useFullscreen 

```JavaScript


import React, { useState, useEffect, useRef, useCallback } from "react";
import "./styles.css";


const useFullscreen = (callback) => {
  const element = useRef();
  const runCb = (isFull) => {
    if (callback && typeof callback === "function") {
      callback(isFull);
    }
  };
  const triggerFull = () => {
    if (element.current) {
      if (element.current.requestFullscreen) {
        element.current.requestFullscreen();
      } else if (element.current.mozRequestFullScrren) {
        element.current.mozRequestFullScrren();
      } else if (element.current.webkitRequestFullscreen) {
        element.current.webkitRequestFullscreen();
      } else if (element.current.msRequestfullscreen) {
        element.current.msRequestfullscreen();
      }
      runCb(true);
      // if (callback && typeof callback === "function") {
      //   callback(true);
      // }
    }
  };
  const exitFull = () => {
    // document.exitFullscreen();
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.mozCancelFullScreen) {
      document.mozCancelFullScreen();
    } else if (document.webkitExitFullscreen) {
      document.webkitExitFullscreen();
    } else if (document.msExitFullscreen) {
      document.msExitFullscreen();
    }
    // if (callback && typeof callback === "function") {
    //   callback(false);
    // }
    runCb(false);
  };
  return { element, triggerFull, exitFull };
};

export default function Hook6() {
  // const [item, setItem] = useState(5);
  const onFullS = (isFull) => {
    console.log(isFull ? "we are full" : "web are small");
  };
  const { element, triggerFull, exitFull } = useFullscreen(onFullS);
  return (
    <div className="App" style={{ height: "1000vh" }}>
      <div ref={element}>
        <img src="http://cafefiles.naver.net/data34/2008/10/4/275/%C6%F7%B8%CB%BA%AF%C8%AF_%B6%F3%B8%E9_0asy0.jpg" />
        <button onClick={exitFull}>Make exit screen</button>
      </div>
      <button onClick={triggerFull}>Make full screen</button>
    </div>
  );
}

```




### useNotification 

```JavaScript



import React, { useState, useEffect, useRef, useCallback } from "react";
import "./styles.css";

const useNotification = (title, options) => {
  // console.log("call useNotification");
  if (!("Notification" in window)) {
    console.log("is");
    return;
  }
  // console.log("useNotification");
  const fireNotif = () => {
    if (Notification.permission !== "granted") {
      Notification.requestPermission().then((permission) => {
        if (permission === "granted") {
          new Notification(title, options);
        } else {
          return;
        }
      });
    } else {
      new Notification(title, options);
    }
  };

  return fireNotif;
};

export default function Hook7() {
  const triggerNotif = useNotification("Can I steal your kimchi ?", {
    body: "i love kimchi"
  });

  return (
    <div className="App">
      <button onClick={triggerNotif}>hello</button>
    </div>
  );
}


```






### useAxios 

```JavaScript


import defaultAxios from "axios";
import { useState, useEffect } from "react";

const useAxios = (opts, axiosInstance = defaultAxios) => {
  const [state, setState] = useState({
    loading: true,
    error: null,
    data: null
  });
  const [trigger, setTrigger] = useState(0);
  if (!opts.url) {
    return;
  }
  const refetch = () => {
    setState({
      ...state,
      loading: true
    });
    setTrigger(Date.now());
  };
  useEffect(() => {
    axiosInstance(opts)
      .then((data) => {
        setState({ ...state, loading: false, data });
      })
      .catch((error) => {
        setState({ ...state, loading: false, error });
      });
  }, [trigger]);
  return { ...state, refetch };
};

export default useAxios;



import React, { useState, useEffect, useRef, useCallback } from "react";
import "./styles.css";
import useAxios from "./useAxios";

export default function Hook8() {
  const { loading, data, error, refetch } = useAxios({
    url:
      "https://cors-anywhere.herokuapp.com/https://yts.am/api/v2/list_movies.json"
  });
  // console.log(
  //   `Loading:${loading}\nError:${error}\nData:${JSON.stringify(data)}`
  // );
  return (
    <div className="App">
      <h1>{data && data.status}</h1>
      <h2>{loading && "Loading"} </h2>
      <h2>{error} </h2>
      <button onClick={refetch}>refetch</button>
    </div>
  );
}

```

