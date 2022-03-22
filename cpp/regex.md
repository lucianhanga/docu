# regex

`\d` - digit 0-9
`\D` - NOT a digit
`\s` - whitespace character 
`\S` - NOT an whitespace character
`\w` - alphanumeric character 0..9 a-z A-Z _
`\W` - NOT an alphanumeric 

`[^a-z]` - not  lower case letter

inside a class the meta character should not be escapted: `[*^$]`


### regex_match

```c++
    const regex r5{ "[a-zA-Z]*" };
    const regex r6{ R"(\w*)" };
    const regex r7{ R"(\w{1,4})" }; // from 1 to 4 alphanumeric characters
    cout << boolalpha << regex_match("moto"s, r5) << endl;
    cout << boolalpha << regex_match("moto"s, r6) << endl;
    cout << boolalpha << regex_match("moto"s, r7) << endl;
```

### regex_replace 

```c++
    cout << endl;
    cout << "replacement" << endl;
    const string s1{ "The xxx should be replaced and this one xxx too." };
    cout << format("\"{}\"\n\"{}\"\n", s1, regex_replace(s1, regex{ R"(x{3})" }, "1234") ) << endl;

```

### regex_search

```c++
    const string s10{ "12345 this is one number and 56789 is the other number." };
    const regex numberReg{ R"(\d+)" };
    smatch matchResult{};
    cout << boolalpha << regex_search(s10, matchResult, numberReg) << endl;
    cout << matchResult.str() << endl;
    matchResult.subfix(); // contains the remaining part 
                          // of the string which was not search yet
```