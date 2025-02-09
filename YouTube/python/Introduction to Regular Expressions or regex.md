string containing a combination of normal characters and special metacharacters that describes pattern to find text or positions within a text

eg: `r'st\d\s\w{3,10}'`

normal characters = st
special metacharacters =\d, \s, \w,  or ideas - {3, 10}

#### Pattern: 
a sequence of characters that maps to words or punctuation

#### Pattern matching usage
- Find and replace text
- Validate strings


```python
	# import regex module
	import re 
	# Find all matches of a pattern
	re.findall (r'regex', string)
	
	re.findall(r"#movies", "Love #movies! I had fun yesterday going to the #movies")
	
	# split string at each match
	re.split (r'regex', string)
	
	re.split(r"!", "Nice Place to eat! I'll come back! Excellent meat!")
	
	# Replace one or many matches with a string
	re.sub(r'regex', new, string)
	
	re.sub(r"yellow", "nice", "I have a yellow car and a yellow house in a yellow neighborhood")
```
### Supported metacharacters

| Meta Characters | Meaning          |
| --------------- | ---------------- |
| \d              | digit            |
| \D              | non - digit      |
| \w              | word             |
| \W              | non - word       |
| \s              | whitespace       |
| \S              | non - whitespace |

### Repetitions
#### Quantifiers
A metacharacter that tells the regex engine how many times to match a character immediately to its left. 

| Quantifiers | Meaning               |
| ----------- | --------------------- |
| +           | once or more times    |
| *           | zero times or more    |
| ?           | zero times or once    |
| {n, m}      | n at least, m at most |
![[regex.pdf]]

![[Advanced Regex.pdf]]

#python #regex




