Q.no.2)  Write a program that abbreviates the string when the length is greater than
16 in a way that fulfills the following requirements:
Input: Sarbham Technology => Output: Sarbham T.
Input: Kathmandu Metropolitan City => Output: Kathmandu M. C.
Input: James Bond => Output: James Bond
Input: Can AlphaGamma Tech => Output: Can A. Tech

Solution: 

```
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

Output: 
```
[LOG]: "Input: Sarbham Technology => Output: Sarbham T." 
[LOG]: "Input: Kathmandu Metropolitan City => Output: Kathmandu M. C." 
[LOG]: "Input: James Bond => Output: James Bond" 
[LOG]: "Input: Can AlphaGamma Tech => Output: Can A. Tech"
[LOG]: "Input: ThisisaverylongTexttocheck City => Output: T. C." 
```

Reasoning:
- I have used recursive solution to this,which can be optimized using memoisation but since this is a simple algorithm, such optimisation is actually not needed and would be regarded as overengineering the solution in my opinion. I had to use the n/2 thing because if after shortening the first time, if the length of the total string is still >16 then we will have to shorten the word which is less then 10 since n=10 by default, this will continue until the total string is less than 16.

Q.no.3) Get an array of ids in ascending order based on the total sum of sales for
each id from the data below.
[{id:am, info:{ sales:{ pen:10; marker:25 }}},
{id:sar, info:{ sales:{ pen:30; marker:15 }}},
{id:bh, info:{ sales:{ pen:25; marker:15 }}}]

Solution:

```
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

Output:

```
[LOG]: "Sorted Ids based on total sum of sales:",  ["am", "bh", "sar"] 
```

Reasoning:

- I first captured the id as key and the total sales as the respective value of id through sums object and then captured the key 

Q.no.4) Find the pairs of array element for which sum is equal to given target value (Two Sum Problem)
Target value : 7

Solution:
```
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

Output:
```
[LOG]: "Resultant pair for target : 7 is",  [[3, 4], [2, 5], [1, 6]] 
```

Reasoning:

- I have opted to use Set here to store unique values and it's average time complexity for it's operation is O(1)




