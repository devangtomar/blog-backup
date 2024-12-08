---
title: "Your Ultimate Regular Expression (Regex) Cheat Sheet 👑😎"
datePublished: Fri Nov 11 2022 06:32:34 GMT+0000 (Coordinated Universal Time)
cuid: clafg7jpi03ll6hnv7w5tgtqp
slug: your-ultimate-regular-expression-regex-cheat-sheet-8d5bf665f455
canonical: https://devangtomar.medium.com/your-ultimate-regular-expression-regex-cheat-sheet-8d5bf665f455
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1668349484874/z9gGvygvz.png
tags: patterns, regex, regular-expressions, regexp, pattern-matching

---

A regular expression (regex) is a pattern in input text that the regex engine attempts to match. A pattern is made up of one or more character literals, operators, or structures. It excels in searching for and manipulating text strings, as well as text file processing. Hundreds of lines of programming code can be readily replaced by a single regex line. This blog will introduce you to basic to sophisticated regex ideas that will aid you in your development work.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349468384/IPT3ccjcq8.png align="left")

### Why Regex? 🙋🏻‍♀️

Regular expressions simplify searching and replacing processes. A frequent use case is finding a substring that matches a pattern and replacing it with something else. One of the most intriguing features is that, once you’ve mastered the syntax, you can use this tool in (almost) any programming language with only minor differences in the support of the most advanced features and syntax versions supported by the engines.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349470045/mz0RP5jqM.png align="left")

### Characters 🔣

The most fundamental regex idea is the character class. It translates a small set of characters into a wider set of characters.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349472015/BXhdfsjH_p.png align="left")

### Groups 🫂

A group expression is used to perform operations on all objects in a group. A group expression can be used to apply an operator to a group or to find a specific text before or after each member of the group. The parentheses are the grouping operator, and the “|” is used to divide the items.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349474106/KZhPQl6Wn.png align="left")

### Quantifiers ⚖️

Quantifiers determine the number of characters or expressions to match. Quantifiers describe the number of instances of a character, group, or character class that must exist in the input for a match to be found.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349476093/Yqg-Mae1bU.png align="left")

### Assertions 🧑🏻‍🏭

Boundaries, which denote the beginnings and endings of lines and words, and other patterns indicating that a match is conceivable are examples of assertions (including look-ahead, look-behind, and conditional expressions).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349477853/kXO9h_6HW.png align="left")

### Flags 🚩

Flags are appended to the end of a regular expression. They are used to alter the behaviour of the regular expression.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349479774/RLqGGRULjw.png align="left")

### Some useful resources 🪴

#### Tips to increase the performance 💡

* **When you require parentheses but not capture, use non-capturing groups.**
    
* **Do a quick check before attempting a match, if the regex is very complex.**  
    Ex : Does an email address contain ‘@’?
    
* **Present the most likely option(s) first.**  
    Ex : light green|dark green|brown|yellow|green|pink leaf
    
* **Minimize the amount of looping.**  
    Ex : aaaaaa+ is faster than a{6,}
    
* **Avoid obvious backtracking**  
    Ex : Mr|Ms|Mrs should be M(?:rs?|s)
    

#### Regex sites I use :

%[https://regex101.com/] 

%[https://regexone.com/] 

### Conclusion 💭

To summarise, regex can be used to match strings of data and can be utilised in a variety of ways. Python has a regex library called re that allows you to do this. If you’re on a Unix machine, you can utilise regular expressions in conjunction with grep, awk, or sed. If you wish to access all of these commands on Windows, you can utilise tools like Cygwin.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668349483306/-ZJfun3KR.png align="left")

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)