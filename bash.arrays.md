# Arrays in bash

Get the folder contents and store them into an array
```bash
export array=( $(ls foldername) )
```

The number of elements of an array
```bash
echo ${#array[@]}
```

Display all array
```bash
echo ${array[@]}
```

Display the first and second elements
```bash
echo ${array[0]}
echo ${array[1]}
```

Get a random index into the array
```bash
export index=$(( $RANDOM % ${#array[@]} ))
```
