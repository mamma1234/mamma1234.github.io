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


## useConfirm && usePreventLeave

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


## useBeforeLeave

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


## useFadeIn

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






## useNetwork

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




## useScroll

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








## useFullscreen 

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




## useNotification 

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






## useAxios 

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

