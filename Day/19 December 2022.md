`19 December 2022`

## **Day 2: What I have Learned**

* * *
## **Denial of Service**:
- Denial of Service is Taking down a system and making it unavailable or using Bad Traffic and attack To take down the system making it unavailable.

## **Regular Expression**:
- Regular Expression is a sequence of characters that specifies a search pattern in text and specifies a set of strings that matches it.

## **Regular Expression Denial of Service**:
- ReDOS(Regular Expression Denial of Service) Due to weakly implemented RegEx Sometimes it is possible to perform a DoS attack by making this expression to evaluate an expression which will make the application work relatively slow.
- Usually this attack is explored and exploited when the source code is available and you can figure out what regular expressions are used in the code at what fields. 
- For example, at the mobile no input field, what is the regex that validates the mobile no input field.
However, you can also try to find this in Black/Gray Box engagements.

## **Method**:
- Open the JavaScript files and search for the "RegExp(" function and try to figure out what function utilize that particular Regex.

## **Library**:
1. This is a good tool to evaluate and identify if the given regex is vulnerable or not. 
This tool will also provide a string that will make the vulnerable RegEx go into potential ReDoS Attacks.
[Here](https://github.com/2bdenny/ReScue).
2. Use this package to easily convert various time formats to milliseconds.
[Here](https://www.npmjs.com/package/ms).

## **Resources to Learn More**:
1. [Regexone](https://regexone.com)
2. [speakerdeck](https://speakerdeck.com/harshbothra/having-fun-with-regex)
3. [javascript info](https://javascript.info/regexp-catastrophic-backtracking)

## **Reports**:
1. [All functions that allow users to specify color code are vulnerable to ReDoS ($1000)](https://hackerone.com/reports/511381).
2. [DigestAuth authentication is vulnerable to regular expression denial of service ($200)](https://hackerone.com/reports/661722).

## **Lesson Notes**:
-  List itemLesson Notes
- abc…	Letters
- 123…	Digits
- \d	Any Digit
- \D	Any Non-digit character
- .	Any Character
- \.	Period
- [abc]	Only a, b, or c
- [^abc]	Not a, b, nor c
- [a-z]	Characters a to z
- [0-9]	Numbers 0 to 9
- \w	Any Alphanumeric character
- \W	Any Non-alphanumeric character
- {m}	m Repetitions
- {m,n}	m to n Repetitions
- *= Zero or more repetitions
- += One or more repetitions
- ?	Optional character
- \s	Any Whitespace
- \S	Any Non-whitespace character
- ^…$	Starts and ends
- (…)	Capture Group
- (a(bc))	Capture Sub-group
- (.*)	Capture all
- (abc|def)	Matches abc or def

