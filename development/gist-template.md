# Matching an Email

In this tutorial we're going to go over basic concepts of RegEx componets(Regular Expressions) to better understand how to match an email using these systems.

## Summary

This regex is a simplified version for basic email validation, and it matches email addresses that follow common patterns but doesn't account for all possible edge cases in email formatting.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

- **`^`:** Start at the beginning of the line.
- **`[a-zA-Z0-9._%+-]+`:** Match one or more characters that can be in an email username.
- **`@`:** Match the "@" symbol.
- **`[a-zA-Z0-9.-]+`:** Match one or more characters that can be in the domain name.
- **`\.`:** Match a literal dot (.) character.
- **`[a-zA-Z]{2,}`:** Match at least two or more letters for the top-level domain (TLD).
- **`$`:** Match the end of the line.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

An anchor in regular expressions is a special character that doesn't match any actual characters in the text. Instead, it marks specific positions in the text. Anchors are used to specify where a certain pattern should appear in the text.

There are two main types of anchors:

**Start Anchor (^):** This anchor asserts that the pattern following it must appear at the very beginning of the text.

**End Anchor ($):** This anchor asserts that the pattern preceding it must appear at the very end of the text.

For example, if you use the pattern `/^Hello/`, it would match the word "Hello" only if it appears at the beginning of the text. Similarly, if you use the pattern `/world$/`, it would match the word "world" only if it appears at the end of the text.

Anchors help you focus on finding patterns in specific positions within the text, rather than just searching for patterns anywhere in the text.

### Quantifiers

Quantifiers are symbols that help you specify the number of occurrences a particular part of the pattern should have in order to match. They give you control over how flexible or strict your pattern matching is. Here are the common quantifiers:

1. `*` (Asterisk): This quantifier means "zero or more." It matches when the preceding element occurs any number of times, including none.

2. `+` (Plus): This quantifier means "one or more." It matches when the preceding element occurs at least once and can repeat more times.

3. `?` (Question Mark): This quantifier means "zero or one." It matches when the preceding element occurs either once or not at all.

4. `{n}` (Curly Braces): This quantifier specifies an exact number of occurrences. It matches when the preceding element appears exactly n times.

5. `{n,}` (Curly Braces with a Comma): This quantifier matches when the preceding element occurs at least n times.

6. `{n,m}` (Curly Braces with Two Numbers and a Comma): This quantifier matches when the preceding element occurs at least n times but no more than m times.

Quantifiers add precision to your regex patterns. For instance, if you're looking for email addresses, you can use + after the username part to ensure there's at least one character there. Or you can use {2,4} after a digit pattern to match numbers that are between two and four digits long.

Quantifiers are like a way to tell the regex engine how many times a certain part of your pattern should be repeated to consider it a match. They're essential for fine-tuning your searches and making your patterns more powerful and specific.

### OR Operator

The "OR" operator, often denoted as `|`, is a tool that helps you search for multiple options within a pattern. It's like having different choices to match in your search.

Imagine you have a box of crayons, and you want to find all the red ones and all the blue ones. Instead of searching for red crayons and then searching again for blue ones, you can use the "OR" operator to combine these searches into a single step.

For example, if you're looking for either "cat" or "dog" in a text, you can create a pattern like `cat|dog`. This pattern means "find either 'cat' or 'dog'." The `|` symbol works as a separator, telling the regex engine that it should match either the expression on the left side or the one on the right side.

Here's another example: imagine you're searching for specific words in an article. You might want to find instances of both "car" and "bike." Instead of creating separate patterns for each word, you can use the "OR" operator like this: `car|bike`.

So, the "OR" operator is like a way to say "I'm interested in this thing or that thing." It's really handy when you want to search for multiple options without having to repeat the same search process over and over again.

### Character Classes

Character classes in regular expressions are like special clubs for characters that have something in common. They help you find specific types of characters in a text without having to list them all individually.

Think of character classes as groups of friends who share something in common. For instance, you might have a group of friends who all like sports, and another group who all like art. Instead of listing every friend's name, you can just say "sports lovers" or "art enthusiasts."

In regex, you use square brackets `[]` to create a character class. Inside the brackets, you put the characters you're interested in. Here are some examples:

1. `[aeiou]`: This character class matches any lowercase vowel (a, e, i, o, u). It's like saying "any one of these characters."

2. `[0-9]`: This character class matches any digit from 0 to 9. It's a shortcut for saying "any digit in this range."

3. `[A-Za-z]`: This character class matches any uppercase or lowercase letter. It's like saying "any letter, whether big or small."

4. `[A-Fa-f0-9]`: This character class matches any hexadecimal digit, meaning any digit from 0 to 9 and any letter from A to F (in both uppercase and lowercase). It's a way to say "any valid hexadecimal digit."

5. `[^0-9]`: This character class with a caret `^` at the beginning is like the opposite. It matches any character that is NOT a digit. It's like saying "anything that's not in this list."

6. `[\s\S]`: This character class matches any whitespace character or any non-whitespace character. It's a way to cover everything.

So, character classes help you group characters by their common traits and make your searches more flexible and concise. Just like grouping friends with similar interests, character classes group characters that share a common purpose in your regular expressions.

### Flags

Flags are special settings or options that you can attach to a regex pattern to modify how it behaves when searching through text. They provide additional control and customization to your regex searches. Flags are typically written as single letters following the closing slash / of the regex pattern.

Here are some common flags used in regex:

1. `i` **(Case-Insensitive):** This flag makes the regex pattern match characters regardless of their case. For example, with the flag `/abc/i`, it would match "abc," "AbC," "aBc," and so on.

2. `g` **(Global):** This flag tells the regex engine to find all matches in the input text rather than stopping after the first match. Without this flag, regex will often stop at the first match it finds.

3. `m` **(Multi-line):** This flag is used when you have text with multiple lines, like a poem or code, and you want to match patterns across lines. It changes the behavior of `^` and `$` to match the start and end of each line instead of just the whole text.

4. `s` **(Single-line or Dot-All):** This flag allows the dot (`.`) in your pattern to match any character, including newline characters (`\n`). Without this flag, the dot typically matches any character except for newlines.

5. `u` **(Unicode):** This flag enables full Unicode matching. It's particularly useful when working with non-ASCII characters or characters from various languages.

6. `y` **(Sticky):** This flag restricts matches to occur only at the current position in the text. It's often used in combination with the global flag `g`.

For example, if you want to perform a case-insensitive and global search for the word "apple" in a text, you'd use the `/apple/ig` regex pattern with the `i` and `g` flags.

Flags help you fine-tune your regular expressions to suit your specific search requirements. They allow you to control case sensitivity, match behavior across lines, and much more, making regex a powerful tool for text processing and pattern matching.

### Grouping and Capturing

Grouping and capturing are features in regular expressions that allow you to organize parts of your pattern and also save or reference those parts for later use. They're like tools that help you keep track of different pieces of information within the text you're searching.

**Grouping:**
Imagine you have a bunch of differently colored marbles mixed together. You want to group them by color to count how many marbles of each color you have. Similarly, in regex, you can use parentheses `()` to create groups that enclose parts of your pattern. These groups help you apply quantifiers or operators to specific portions of your pattern.

For example, the regex pattern `(ab)+` groups the characters "ab" together. The `+` outside the group means "one or more" of the entire group `(ab)`.

**Capturing:**
Now, imagine you not only want to group the marbles by color but also want to remember the count of each color. In regex, capturing groups not only group parts of your pattern but also "capture" and remember the text that matches that group. You can then refer to captured groups later in your regex or during replacements.

For instance, if you have the pattern `(apple|banana)` pie, and you apply it to the text "apple pie is delicious," the capturing group `(apple|banana)` captures "apple" because it's the part that matched. You can then reference the captured group using special syntax, like `\1`, to use it in replacements.

To summarize:

- **Grouping `( )`:** Helps you apply quantifiers or operators to specific parts of your pattern. `(ab)+` means "one or more occurrences of 'ab'."

- **Capturing `( )`:** Groups and remembers the text that matches that part of the pattern. `(apple|banana)` captures either "apple" or "banana" and allows you to reference it using special syntax like `\1`.

Grouping and capturing are essential for managing complexity in your regular expressions and for extracting specific pieces of information from the text you're working with. Just as sorting marbles by color helps you organize them better, grouping and capturing in regex help you manage and manipulate text more effectively.

### Bracket Expressions

Bracket expressions, also known as character classes, are a way to specify a set of characters you're interested in within a regular expression. They're like a special container for characters that you want to match.

Think of it as creating a custom group of characters, kind of like having a box of favorite toys. You can put all your favorite toys in this box, and whenever you're looking for a toy, you'll only look inside this box.

In regular expressions, bracket expressions are enclosed in square brackets `[ ]`. Here are a few examples:

1. `[aeiou]`: This bracket expression matches any lowercase vowel. It's like saying "any one of these characters: a, e, i, o, u."

2. `[0-9]`: This bracket expression matches any digit from 0 to 9. It's like saying "any digit in this range."

3. `[A-Za-z]`: This bracket expression matches any uppercase or lowercase letter. It's like saying "any letter, whether big or small."

4. `[A-Fa-f0-9]`: This bracket expression matches any hexadecimal digit, meaning any digit from 0 to 9 and any letter from A to F (in both uppercase and lowercase). It's a way to say "any valid hexadecimal digit."

5. `[^0-9]`: This bracket expression with a caret `^` at the beginning is like the opposite. It matches any character that is NOT a digit. It's like saying "anything that's not in this list."

Bracket expressions help you be specific about the characters you want to match. Just like having a special box for your favorite toys, bracket expressions create a "box" of characters you're interested in, making your regular expressions more precise and powerful.

### Greedy and Lazy Match

**Greedy Matching:**
Imagine you're at a buffet with lots of different foods, and you want to get as much food as possible. You keep grabbing items until you can't eat anymore. Greedy matching in regular expressions is a bit like this – it tries to match as much text as it can while still allowing the overall pattern to match.

For instance, let's say you have the text "abcdef" and you use the pattern `/a.*d/`. The `.*` part is a greedy match, so it would try to grab as many characters as possible between "a" and "d." In this case, it would match the whole text "abcdef," even though you might have expected it to stop at "ad."

**Lazy (Non-Greedy) Matching:**
Now, imagine you're reading a book and you're in a hurry. You just want to get a quick summary of each chapter without reading all the details. Lazy matching in regular expressions is like this – it matches as little text as possible while still making the pattern match.

Using the same text "abcdef" and pattern `/a.*?d/`, the `.*?` part is a lazy match. It would try to grab as few characters as possible while still allowing the pattern to match. In this case, it would match "ad" – the shortest possible sequence that fits the pattern.

In summary:

**Greedy Matching:** Grabs as much text as possible while still making the overall pattern match.

**Lazy (Non-Greedy) Matching:** Grabs as little text as possible while still making the pattern match.

Greedy and lazy matching are important concepts because they influence how your regular expressions behave, especially when there are repeated patterns in the text. Depending on your needs, you can choose the appropriate type of matching to get the desired results in your pattern searches.

### Boundaries

Boundaries are like invisible lines that help you define where specific patterns or characters should or shouldn't appear within the text you're searching. They act as markers to control exactly where your pattern should start or end its search.

Think of boundaries as the edges of a puzzle piece – they define where that piece fits perfectly with the others. Similarly, in regex, boundaries define where your pattern should fit perfectly within the text.

Here are two common types of boundaries:

**Word Boundary (\b):** The word boundary is like a line that separates words in a text. It's not an actual character; it's a position. Using `\b` in your regex pattern allows you to match patterns that occur at the beginning or end of a word. For example, `\bword\b` would match only the standalone word "word" and not "wording" or "password."

**Line Start and End (`^` and `$`):** The caret `^` and dollar sign `$` are used to represent the start and end of a line in your text. `^` matches the very beginning of a line, and `$` matches the very end of a line. For instance, `^Hello` would match "Hello" only if it appears at the beginning of a line.

Using these boundaries helps you create more precise and controlled searches. They ensure that your pattern only matches in the specific positions you want, making your regular expressions more accurate and effective. Just like puzzle piece edges help you fit the pieces together correctly, regex boundaries help you fit your patterns perfectly within the text.

### Back-references

Back-references in regular expressions allow you to refer to and reuse parts of your pattern that you've already matched. They're like placeholders that remember what you've found and allow you to use that information later in your regex.

Think of it as taking notes while reading a book. When you find something important, you jot it down on a piece of paper so you can easily refer back to it later.

In regex, you use parentheses `()` to create capturing groups. When you capture something with parentheses, you can later refer to it using backreferences.

For example, let's say you have the pattern `(\w+)\s+\1.` The first capturing group `(\w+)` captures one or more word characters, and then `\s+` matches one or more spaces. The `\1` is a backreference to the first capturing group, meaning it will match whatever was captured by that group earlier.

If you use this pattern on the text "apple apple," it will match the entire phrase because the backreference `\1` ensures that the same word appears twice.

In simple terms:

- **Capturing Group (`()`):** Like taking notes on important information while reading.
- **Back-reference (`\1`, `\2`, etc.):** Referring back to those notes to use the same information again.
  Backreferences are useful when you want to find repeated patterns or ensure that certain parts of your text match each other. They save you from writing redundant patterns and help you efficiently work with repeating data.

### Look-ahead and Look-behind

Look-ahead and look-behind are advanced concepts in regular expressions that allow you to check for specific conditions before or after a particular pattern, without actually including those conditions in the match. They're like sneak peeks that help you decide whether a certain part of your pattern should match.

**Look-ahead (`(?=...)`):**
Think of look-ahead as a peek into the future. It's like checking what's coming up next before deciding whether to match the current pattern. If you're baking cookies and want to make sure you have enough chocolate chips, you might look ahead in the recipe to see if you need more.

In regex, a positive look-ahead is written as `(?=...)`. For example, `apple(?= pie)` would match "apple" only if it's followed by the word "pie." The look-ahead `(?= pie)` checks if "pie" comes after "apple," without including "pie" in the actual match.

**Negative Look-ahead (`(?!...)`):**
This is like looking ahead to make sure something doesn't happen. Using the cookie analogy, it's like checking the recipe to make sure there are no onions in your chocolate chip cookies.

In regex, a negative look-ahead is written as `(?!...)`. For instance, `apple(?! pie)` would match "apple" only if it's not followed by the word "pie." The negative look-ahead `(?! pie)` checks if "pie" is not present after "apple."

**Look-behind (`(?<=...)`):**
Look-behind is similar, but it checks what's behind the current position in the text. It's like checking the ingredients you've already used before deciding what to add next.

In regex, a positive look-behind is written as `(?<=...)`. For example, `(?<=good )morning` would match "morning" only if it's preceded by the words "good." The look-behind `(?<=good )` checks if "good" comes before "morning."

**Negative Look-behind (`(?<!...)`):**
This is like checking that something isn't behind you before you take a step. In regex, a negative look-behind is written as `(?<!...)`.

In simple terms:

**Look-ahead (`(?=...)`):** Checking what comes after the pattern.

**Negative Look-ahead (`(?!...)`):** Checking that something doesn't come after the pattern.

**Look-behind (`(?<=...)`):** Checking what comes before the pattern.

**Negative Look-behind (`(?<!...)`):** Checking that something doesn't come before the pattern.

Look-ahead and look-behind are powerful tools that help you add complex conditions to your patterns without including those conditions in the actual match.

## Author

Brendan Aper, brings craftsmanship from the world of contracting into the realm of technology. Juggling hammers and lines of code, he's on a dual journey of creating physical structures and digital solutions. Currently residing in the charming city of Bend, Oregon, Brendan draws inspiration from the natural beauty that graces his surroundings. As he embarks on his path of learning computer programming and web development through the edX School's Bootcamp, Brendan bridges the gap between the tangible and the virtual, creating a dynamic fusion of skills.

Follow on [GitHub](https://github.com/brendan-aper)
