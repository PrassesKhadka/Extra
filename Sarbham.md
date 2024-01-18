## Q.no.1) Write a program that gives a list of unique countries from the list below.## 
[
{
"countries": ["Nepal"],
"animals": "robin"
},
{
"countries": ["Germany", "Italy", "China"],
"animals": "panther"
},
{
"countries": ["Argentina", "Italy", "Nepal", "Spain"],
"animals": "goldfish"
}
]

```c
Solution:

const data = [
    { "countries": ["Nepal"], "animals": "robin" },
    { "countries": ["Germany", "Italy", "China"], "animals": "panther" },
    { "countries": ["Argentina", "Italy", "Nepal", "Spain"], "animals": "goldfish" }
];

const uniqueCountries = new Set();

data.forEach(entry => {
    entry.countries.forEach(country => {
        uniqueCountries.add(country);
    });
});

const uniqueCountriesArray = Array.from(uniqueCountries);
console.log("The list of Unique Countries are: " + uniqueCountriesArray.join(","));
```

```c
Output:
[LOG]: "The list of Unique Countries are: Nepal,Germany,Italy,China,Argentina,Spain"
```

Reasoning:
> I have used Set data structure as it only lets unique entry and discards any repeated element. Also, operations of Set takes an average of O(1) time complexity. 

## Q.no.2)  Write a program that abbreviates the string when the length is greater than16 in a way that fulfills the following requirements:
Input: Sarbham Technology => Output: Sarbham T.
Input: Kathmandu Metropolitan City => Output: Kathmandu M. C.
Input: James Bond => Output: James Bond
Input: Can AlphaGamma Tech => Output: Can A. Tech## 

```c
Solution:

function outputString(inputString:string,n=10) {
    const wordsArray = inputString.split(' ');

    if (inputString.length <= 16) 
        return inputString;
    
    if (wordsArray.length === 1) 
        return inputString.substring(0,16) + ".";
    
    const outputArray=wordsArray.map((word,index)=>{
        if(index===0 && n>0)
            return word; 
        if(word.length<n)
               return word;
        else
            return word.substring(0,1) + "."

    })

    return outputString(outputArray.join(" "),n/2);
}

const inputStr1 = "Sarbham Technology";
const inputStr2 = "Kathmandu Metropolitan City";
const inputStr3 = "James Bond";
const inputStr4 = "Can AlphaGamma Tech";
const inputStr5 = "ThisisaverylongTexttocheck City";

const outputStr1 = outputString(inputStr1);
const outputStr2 = outputString(inputStr2);
const outputStr3 = outputString(inputStr3);
const outputStr4 = outputString(inputStr4);
const outputStr5 = outputString(inputStr5);

console.log(`Input: ${inputStr1} => Output: ${outputStr1}`);
console.log(`Input: ${inputStr2} => Output: ${outputStr2}`);
console.log(`Input: ${inputStr3} => Output: ${outputStr3}`);
console.log(`Input: ${inputStr4} => Output: ${outputStr4}`);
console.log(`Input: ${inputStr5} => Output: ${outputStr5}`);
```

```c
Output:

[LOG]: "Input: Sarbham Technology => Output: Sarbham T." 
[LOG]: "Input: Kathmandu Metropolitan City => Output: Kathmandu M. C." 
[LOG]: "Input: James Bond => Output: James Bond" 
[LOG]: "Input: Can AlphaGamma Tech => Output: Can A. Tech"
[LOG]: "Input: ThisisaverylongTexttocheck City => Output: T. C." 
```

Reasoning:
- I have used recursive solution to this,which can be optimized using memoisation but since this is a simple algorithm, such optimisation is actually not needed and would be regarded as overengineering the solution in my opinion. I had to use the n/2 thing because if after shortening the first time, if the length of the total string is still >16 then we will have to shorten the word which is less then 10 since n=10 by default, this will continue until the total string is less than 16.

## Q.no.3) Get an array of ids in ascending order based on the total sum of sales for
each id from the data below.
[{id:am, info:{ sales:{ pen:10; marker:25 }}},
{id:sar, info:{ sales:{ pen:30; marker:15 }}},
{id:bh, info:{ sales:{ pen:25; marker:15 }}}]## 


```c
Solution:

const data = [
    { id: 'am', info: { sales: { pen: 10, marker: 25 } } },
    { id: 'sar', info: { sales: { pen: 30, marker: 15 } } },
    { id: 'bh', info: { sales: { pen: 25, marker: 15 } } }
];

function getResult(data) {
    const sums = {};
    data.forEach(item => {
        const id = item.id;
        const sales = Object.values(item.info.sales);
        sums[id] = sales.reduce((pen, marker) => pen + marker, 0);
    });

    const result = Object.keys(sums).sort((a, b) => sums[a] - sums[b]);
    return result;
}

const sortedIds = getResult(data);
console.log("Sorted Ids based on total sum of sales:", sortedIds);
```


```c
Output:

[LOG]: "Sorted Ids based on total sum of sales:",  ["am", "bh", "sar"] 
```

Reasoning:

- I first captured the id as key and the total sales as the respective value of id through sums object and then captured the key 

## Q.no.4) Find the pairs of array element for which sum is equal to given target value (Two Sum Problem)
Target value : 7## 

```c
Solution:

function getResult(data, target) {
    const result = [];
    const seenElements = new Set();

    for (let num of data) {
        const complement = target - num;

        if (seenElements.has(complement)) {
            result.push([complement, num]);
        }

        seenElements.add(num);
    }

    return result;
}

const data= [1, 2, 3, 4, 5, 6, 7, 8, 9];
const target= 7;

const resultPair = getResult(data, target);
console.log(`Resultant pair for target : ${target} is`, resultPair);
```

```c
Output:

[LOG]: "Resultant pair for target : 7 is",  [[3, 4], [2, 5], [1, 6]] 
```

Reasoning:

- I have opted to use Set here to store unique values and it's average time complexity for it's operation is O(1)

## Q.no.5) Remove duplicates from an array and return unique values of that array and
also array of all duplicates.
Array: [5, 5, 1, 2, 3, 4, 6, 4, 7, 7, 8, 9, 10, 11, 9]## 

```c
Solution:

function removeDuplicates(data) {
    const uniqueValues = [];
    const duplicates = [];

    const uniqueSet = new Set();

    for (const value of data) {
        if (uniqueSet.has(value)) {
            duplicates.push(value);
        } else {
            uniqueValues.push(value);
            uniqueSet.add(value);
        }
    }

    return {
        uniqueValues,
        duplicates
    };
}

const data= [5, 5, 1, 2, 3, 4, 6, 4, 7, 7, 8, 9, 10, 11, 9];
const result = removeDuplicates(data);

console.log("Duplicates:", result.duplicates);
console.log("Unique Values:", result.uniqueValues);
```

```c
Output:

[LOG]: "Unique Values:",  [5, 1, 2, 3, 4, 6, 7, 8, 9, 10, 11] 
[LOG]: "Duplicates:",  [5, 4, 7, 9] 
```

## Q.no.6) Check if two strings are anagrams of each other.
E.g. tuna is anagram of aunt.## 

```c
Solution:

function isAnagram(str1:string,str2:string){
    if(str1.length!=str2.length)
        return -1;

    const sortedStr1=str1.split("").sort().join("")
    const sortedStr2=str2.split("").sort().join("")

    if(sortedStr1!=sortedStr2)
        return -1;

    return 1
}

const result=isAnagram("tuna","aunt")
console.log(result ? "Anagram of each other" : "Not anagram of each other)
```

```c
Output:

[LOG]: Anagram of each other
```

## Q.no.7) Write a program to reverse words in a given sentence.
E.g. Hi, sarbham => ,ih mahbras.## 

```c
Solution:

function getReverse(str:string){
    const strArray=str.split(" ")
    const reverseArray=strArray.map((word:string)=>word.split("").reverse().join(""))
    const reverseString=reverseArray.join(" ")
    return reverseString;
}

const str="Hi, sarbham"
const result=getReverse(str);
console.log(`The reverse string for ${str} is: ` + result)
```

```c
Output:

[LOG]: "The reverse string for Hi, sarbham is: ,iH mahbras" 
```

## Q.no.8) Write a multiply function which outputs the result as shown below with 3
given parameters in 3 function calls.
E.g. console.log(multiply(2)(3)(4)) => 24
console.log(multiply(5)(2)(1)) => 10## 

```c
Solution:

function multiply(x) {
    // Initial result is the first parameter
    let result = x;
    return function innerMultiply(y){
        result*=y;
        return function moreInnerMultiply(z){
            result*=z;
            return result;
        }
    }
}

console.log(multiply(2)(3)(4));  
console.log(multiply(5)(2)(1));  
```

```c
Output:

[LOG]: 24 
[LOG]: 10 
```

## Q.no.9) Compute asked data from the given array.## 
```
let student =[
{name:"Ram",age:16,marks:80},
{name:"Henry",age:15,marks:69},
{name:"John",age:16,marks:35},
{name:"Robin",age:14,marks:45},
{name:"Hari",age:13,marks:65},
{name:"Sara",age:15,marks:72},
];
```
Solution:

## a) Print the names of students who scored more than 60## 

```c
const result=student.filter((obj)=>obj.marks>60).map((filteredData)=>filteredData.name)
console.log("The names of students who scored more than 60 are:" + result.join(","))
```

```c
Output:

[LOG]: "The names of students who scored more than 60 are:Ram,Henry,Hari,Sara"
```

## b) Print student’s rollNumber along with their student frequency.## 

Solution:
```c

```

## c) Print list for students with marks greater than 60 after 20 marks have been added to
those who scored less than 50.## 

```c
student.forEach((obj)=>{
    if(obj.marks<50)
        obj.marks+=60
})
const result=student.filter((obj)=>obj.marks>60).map((filteredData)=>filteredData.name)
console.log("The names of students who scored more than 60 are:" +result.join(","))
```
```c
Output:

[LOG]: "The names of students who scored more than 60 are:Ram,Henry,John,Robin,Hari,Sara" 
```

## Q.no.10) Write output of the following Promise chains.## 

## a) Promise.resolve("hello,").then((result) => result + " sarbham")
.then((result) => console.log(result)).catch((err) =>
console.error(err));## 

```c
hello, sarbham
```

## b) Promise.all([Promise.resolve(1), Promise.resolve(2),
Promise.resolve(3)]).then((results) => console.log(results))
.catch((err) => console.error(err));## 

```c
[1,2,3]
```

## c) Promise.race([new Promise((resolve) => { setTimeout(() =>
resolve(1), 1000); }), Promise.resolve(2), Promise.reject(new
Error(3))]).then((result) => console.log(result)).catch((err) =>
console.error(err));## 

```c
2
```
