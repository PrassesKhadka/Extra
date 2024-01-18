Q.no.2) Write a program that abbreviates the string when the length is greater than
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
```

Reasoning:
- I have used recursive solution to this,which can be optimized using memoisation but since this is a simple algorithm, such optimisation is actually not needed and would be regarded as overengineering the solution in my opinion. I had to use the n/2 thing because if after shortening the first time, if the length of the total string is still >16 then we will have to shorten the word which is less then 10 since n=10 by default, this will continue until the total string is less than 16.
