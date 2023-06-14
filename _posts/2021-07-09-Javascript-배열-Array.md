---
layout: post
title: 'Javascript-배열-Array'
description:
headline:
modified: 2021-07-09
category: Laguage
imagefeature:
tags: [Javascript-배열-Array]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Record

## 개념

-   자료구조

## 목차

-   [forEach](#forEach)
-   [join](#join)
-   [split](#split)
-   [reverse](#reverse)
-   [slice](#slice)
-   [find](#find)
-   [filter](#filter)
-   [map](#map)
-   [some every](#some-every)
-   [quiz](#quiz)

### forEach

-   thisArg 매개변수(this)를 forEach()에 제공했기에, callback은 전달받은 this의 값을 자신의 this 값으로 사용할 수 있습니다.
    -   arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])

```JavaScript
fruits.forEach((fruit) => console.log(fruit, second), second);
```

### join

```JavaScript
// Q1. make a string out of an array
{
  const fruits = ['apple', 'banana', 'orange'];
  const result = fruits.join(',');
  console.log(result);
}
```

### split

```JavaScript
// Q2. make an array out of a string
{
  const fruits = '🍎, 🥝, 🍌, 🍒';
  const result = fruits.split(',');
  console.log(result);
}
```

### reverse

```JavaScript
// Q3. make this array look like this: [5, 4, 3, 2, 1]
{
  const array = [1, 2, 3, 4, 5];
  const result = array.reverse();
  console.log(result);
  console.log(array);
}
```

### slice

```JavaScript
// Q4. make new array without the first two elements
{
  const array = [1, 2, 3, 4, 5];
  const result = array.slice(2, 5);
  console.log(result);
  console.log(array);
}
```

### find

```JavaScript
const fruits =  ['1', '2', '1']
const findedata= fruits.find((value, index)=>
    value === '1'
)
console.log(findedata);

$1



class Student {
  constructor(name, age, enrolled, score) {
    this.name = name;
    this.age = age;
    this.enrolled = enrolled;
    this.score = score;
  }
}
const students = [
  new Student('A', 29, true, 45),
  new Student('B', 28, false, 80),
  new Student('C', 30, true, 90),
  new Student('D', 40, false, 66),
  new Student('E', 18, true, 88),
];

// Q5. find a student with the score 90
{
  const result = students.find((student) => student.score === 90);
  console.log(result);
}

```

### filter

```JavaScript
const fruits =  ['1', '2', '1']
const findedata= fruits.filter((value, index)=>
    value === '1'
)
console.log(findedata);

$[ '1', '1' ]


// Q6. make an array of enrolled students
{
  const result = students.filter((student) => student.enrolled);
  console.log(result);
}
```

### map

```JavaScript
const fruits =  ['1', '2', '1']
const findedata2= fruits.map((value, index)=>
    value + 333
)
console.log(findedata2);

$[ '1333', '2333', '1333' ]



// Q7. make an array containing only the students' scores
// result should be: [45, 80, 90, 66, 88]
{
  const result = students.map((student) => student.score);
  console.log(result);
}
```

### some every

```JavaScript
// Q8. check if there is a student with the score lower than 50
{
  console.clear();
  const result = students.some((student) => student.score < 50);
  console.log(result);

  const result2 = !students.every((student) => student.score >= 50);
  console.log(result2);
}
console.clear();
```

### quiz

```JavaScript

// Q9. compute students' average score
{
  const result = students.reduce((prev, curr) => prev.score + curr.score);
  console.log(result / students.length);
}


// Q10. make a string containing all the scores
// result should be: '45, 80, 90, 66, 88'
{
  const result = students
    .map((student) => student.score)
    .filter((score) => score >= 50)
    .join();
  console.log(result);
}

// Bonus! do Q10 sorted in ascending order
// result should be: '45, 66, 80, 88, 90'
{
  const result = students
    .map((student) => student.score)
    .sort((a, b) => b - a)
    .join();
  console.log(result);
}
```
