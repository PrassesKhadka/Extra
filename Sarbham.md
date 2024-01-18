## Q.no.1) Write a program that gives a list of unique countries from the list below.
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

**Reasoning:**
> I have used Set data structure as it only lets unique entry and discards any repeated element. Also, operations of Set takes an average of O(1) time complexity. 

<br>

## Q.no.2)  Write a program that abbreviates the string when the length is greater than16 in a way that fulfills the following requirements:
Input: Sarbham Technology => Output: Sarbham T.
Input: Kathmandu Metropolitan City => Output: Kathmandu M. C.
Input: James Bond => Output: James Bond
Input: Can AlphaGamma Tech => Output: Can A. Tech

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

**Reasoning:**
> I have used recursive solution to this,which can be optimized using memoisation but since this is a simple algorithm, such optimisation is actually not needed and would be regarded as overengineering the solution in my opinion. I had to use the n/2 thing because if after shortening the first time, if the length of the total string is still >16 then we will have to shorten the word which is less then 10 since n=10 by default, this will continue until the total string is less than 16.
> Also i have not used the nested if else if block but rather chosen a cleaner and more readable approach like above.

<br>

## Q.no.3) Get an array of ids in ascending order based on the total sum of sales for
each id from the data below.
[{id:am, info:{ sales:{ pen:10; marker:25 }}},
{id:sar, info:{ sales:{ pen:30; marker:15 }}},
{id:bh, info:{ sales:{ pen:25; marker:15 }}}]

```c
Solution:

const data = [
    { id: "am", info: { sales: { pen: 10, marker: 25 } } },
    { id: "sar", info: { sales: { pen: 30, marker: 15 } } },
    { id: "bh", info: { sales: { pen: 25, marker: 15 } } }
];

const totalSales = data.map(item => ({
    id: item.id,
    totalSales: Object.values(item.info.sales).reduce((acc, sale) => acc + sale, 0)
}));

const sortedIds = totalSales.sort((a, b) => a.totalSales - b.totalSales).map(item => item.id);
console.log("Sorted ids based on total sales:" + sortedIds.join(,);
```
```c
Output:

[LOG]: "Sorted ids based on total sales:am,bh,sar" 
```

**Reasoning:**

> I used the map function to create a new array totalSales. For each element in the original data array, it calculates the total sales by summing up the values in the sales object using reduce. The result is an array of objects containing id and totalSales properties.The sort function is then applied to the totalSales array, ordering the objects based on the totalSales property in ascending order.Another map operation is performed to extract only the id values from the sorted array, resulting in output.

<br>

## Q.no.4) Find the pairs of array element for which sum is equal to given target value (Two Sum Problem). Here: Target value : 7 

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

**Reasoning:**

> I have opted to use Set here to store unique values and it's average time complexity for it's operation is O(1).For each element num, i have calculated the complement by subtracting num from the target value. The complement is the value that, when added to num, results in the target value.Then we check for Complement in Set:If the complement is found in the seenElements set, it means a pair has been found, and that pair is added to the result array.Regardless of whether a pair is found or not, the current num is added to the seenElements set to ensure it's available for future iterations.

<br>

## Q.no.5) Remove duplicates from an array and return unique values of that array and also array of all duplicates.
Array: [5, 5, 1, 2, 3, 4, 6, 4, 7, 7, 8, 9, 10, 11, 9]

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
**Reasoning**
> I have opted to use Set here to store unique values and it's average time complexity for it's operation is O(1).For each value,we check whether the value is already present in the uniqueSet or not.If it is present, the value is a duplicate, and it is added to the duplicates array.If it is not present, the value is unique, and it is added to both the uniqueValues array and the uniqueSet.Then we get the resultant output.

<br>

## Q.no.6) Check if two strings are anagrams of each other.
E.g. tuna is anagram of aunt.

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

**Reasoning**
> Here, if the length of the two string is not equal it will return false, if not these two strings will be sorted in it's ascending order and compared, if they are not equal, it will return false else true will be returned.

<br>

## Q.no.7) Write a program to reverse words in a given sentence.
E.g. Hi, sarbham => ,ih mahbras.

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

**Reasoning**
> Here, I have used split to keep each word of the string in an array and then map over this array and reverse each word using split(to split each letter of the word in an array) and then reverse the array and then again join it, to give us the reversed word in an array which is then joined to form the resultant string.

<br>

## Q.no.8) Write a multiply function which outputs the result as shown below with 3 given parameters in 3 function calls.
E.g. console.log(multiply(2)(3)(4)) => 24
console.log(multiply(5)(2)(1)) => 10

```c
Solution:

const multiply=num1=>num2=>num3=>num1*num2*num3

console.log(multiply(2)(3)(4));  
console.log(multiply(5)(2)(1));  
```

```c
Output:

[LOG]: 24 
[LOG]: 10 
```
**Reasoning**
> Here, I have used currying using ES6 syntax in JavaScript for a more readable code. In this curried version of multiply function, each function takes one argument and returns another function until all the arguments are collected, and the final result is calculated. It is basically doing like the code below :
> ``` function multiply(x) {
    let result = x;
    return function innerMultiply(y){
        result*=y;
        return function moreInnerMultiply(z){
            result*=z;
            return result;
        }
    }
}
```
<br>

## Q.no.9) Compute asked data from the given array.

let student =[
{name:"Ram",age:16,marks:80},
{name:"Henry",age:15,marks:69},
{name:"John",age:16,marks:35},
{name:"Robin",age:14,marks:45},
{name:"Hari",age:13,marks:65},
{name:"Sara",age:15,marks:72},
];

Solution:

### a) Print the names of students who scored more than 60

```c
const result=student.filter((obj)=>obj.marks>60).map((filteredData)=>filteredData.name)
console.log("The names of students who scored more than 60 are:" + result.join(","))
```

```c
Output:

[LOG]: "The names of students who scored more than 60 are:Ram,Henry,Hari,Sara"
```

**Reasoning**
> Here i have used filtered which results in an array of object whose marks is >60 which is again chained with map which returns an array of name of student who has scored >60 from the previous filter. At last i have joined the string of array together segregating using comma(,) to give the output.

### b) Print student’s rollNumber along with their student frequency.

Solution:
```c

```
**Reasoning**
> The question is unclear.

### c) Print list for students with marks greater than 60 after 20 marks have been added to those who scored less than 50.

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
**Reasoning**
> Here, I have first updated the student array by adding +20 marks to those student who scored less than 50 using forEach since it doesnot return anything and just iterates over the array and then the new updated student array is filtered to give us the array of students who have scored >60 which is then mapped to return an array of the resultant name . I have used join to join each string/elemen/word in the array and segregate them using ,(comma).

<br>

## Q.no.10) Write output of the following Promise chains.

### a) Promise.resolve("hello,").then((result) => result + " sarbham").then((result) => console.log(result)).catch((err) => console.error(err));

```c
hello, sarbham
```
**Reasoning**
> Here once Promise is resolved, .then is triggered and then result i.e "hello," is concataneted with " sarbham" and when this promise is also resolved, the result is console logged to give us the above output.

### b) Promise.all([Promise.resolve(1), Promise.resolve(2),Promise.resolve(3)]).then((results) => console.log(results)).catch((err) => console.error(err));

```c
[1,2,3]
```
**Reasoning**
> Here only when all the promises in the array is resolved .then will be trigerred and the resolved value is console.logged by .then which will output the array of resolved promises values.

### c) Promise.race([new Promise((resolve) => { setTimeout(() => resolve(1), 1000); }), Promise.resolve(2), Promise.reject(new Error(3))]).then((result) => console.log(result)).catch((err) =>console.error(err));

```c
2
```
**Reasoning**
> The promise which gets resolved first among all the promises in the array will be returned by Promise.race and it' resove value will be then console.logged here 2 will be resolved first and then console.logged which is the result.
