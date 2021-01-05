# Bash Scripting How Tos and Exercises

## Exercises

For answers, click [here](#answers).

1. Create 1000 files which start with *myfiles_* and end with a number from 1 to 1000 with zero padding such as *myfiles_0001*, *myfiles_0002* and so on.

2. How many files will be created by running this command?:\
`touch myfiles_{A..D}_{00..100..5}`

3. What is the output of this command?:\
 `echo {1..11..2}`

4. How to create four files named Banana, Orange, Apple and Peach at once?

5. How to force *cp* command to show the report of successfully copied files?

6. How to ask *cp* command to save successful copies in *success.txt* and errors in *errors.txt* files?
    `cp -v * ./backup/`

7. How to redirect both success and error messages to a file?

8. How to get rid of the output of a command completely?

9. What does this command do?\
    `grep -i break-in auth.log | awk {'print $12'}`

10. How to use *grep* and *cut* to get the average ping time (14.529) from the following output?

    ```bash
    $ ping -c 10 google.com
    PING google.com (172.217.165.14) 56(84) bytes of data.
    64 bytes from yyz12s06-in-f14.1e100.net (172.217.165.14): icmp_seq=1 ttl=117 time=17.3 ms

    --- google.com ping statistics ---
    10 packets transmitted, 10 received, 0% packet loss, time 9013ms
    rtt min/avg/max/mdev = 9.644/14.529/28.914/5.160 ms
    ```

11. If HOSTNAME variable is ubuntu, what is the output of following commands?

    ```bash
    echo '$HOSTNAME is the name of this computer'
    echo "$HOSTNAME is the name of this computer"
    ```

12. How to assign a value containing a space to a variable?

13. What does the value of `echo $SECONDS` show when called inside a script?

14. What is the output of `echo $0` inside a script?

15. How to get the number of minutes the current bash session has been running?

16. What is the result of following commands?

    ```bash
    f=$((5/2))
    echo $f
    g=$(echo 5/2 | bc -l )
    echo $g
    ```

17. What is the output of following script?

    ```bash
    [[ "cat" == "cat" ]]
    echo $?
    ```

18. How about this?

    ```bash
    [[ 20 > 100 ]]
    echo $?
    ```

19. How to compare the integer values of 20 and 100?

20. What does the following comparison mean? `[[ -z $a ]]`

21. How to get the length of a string variable such as `name=Amir`?

22. If `name=AmirTajik`, what is the result of `d=${name: -5} && echo $d`

23. What is the result of following commands?

    ```bash
    letters="a b b c d d"
    echo ${letters/a/e}
    echo ${letters/#a/e}
    echo ${letters/%a/e}
    ```

24. How to replace all the instances of letter *b* with *f* in letters variable?\
    `letters="a b b c d d"`

25. What is the output?

    ```bash
    people="Alen Ada Amir Rumi"
    echo ${people/A*/programmer}
    ```

26. How to define an empty array?

27. How to access the third variable of array *b*?

28. Output?

    ```bash
    b=("aa" "bb" "cc")
    b[5]="ee"
    echo $b
    ```

29. How to echo all elements of an array?

30. How to access the last element of an array?

31. What do we call Python-like dictionaries in Bash?

32. Define an associative array named mytheme. Add a *color* key with value *blue* to it.

33. How to empty a file?

34. How to show all values of an associative array?

35. How to show all keys of an associative array?

36. Suppose we have the following associative array.

    ```bash
    declare -A arr
    arr["name"]="Amir Tajik"
    arr["career"]="programmer"
    ```

    Write a bash script with following desired output:

    ```bash
    name: Amir Tajik
    career: programmer
    ```

37. How to loop through all the arguments passed to a function?

38. Write a one-line function that accepts two integers and returns the first value to the power of the second one.\
    So `power 2 3` returns *8*.

39. How to get the number of variables passed to a function or command?

## Answers

1. `touch myfiles_{01..1000}` padding works in bash 4 and above

2. 84 files will be created since A,D,0, and 100 will be considered.

    ```bash
    files_D_000
    files_D_001
    files_D_002
    ...
    files_D_100
    ```

    >Use `$ ls -1 | wc -l` to get the numer of files and directories inside the current directory. Note that after *ls* is *1 (one)* not letter *l*.

3. bash includes the last item in the range (unlike Python)

    ```bash
    $ echo {1..11..2}
    1 3 5 7 9 11

    $ python -c "for i in (range(1,11,2)): print(i)"
    1
    3
    5
    7
    9
    ```

4. `touch {Banana,Orange,Apple,Peach}`\
    There should not be any spaces between the file names.

    >In case of the *touch* command, it also works without brace expansion:\
    `touch Banana Orange Apple Peach`

5. Using the *-v* flag:

    ```bash
    $ cp -v apple apple_copy
    'apple' -> 'apple_copy'
    ```

6. `cp -v * ./backup/ 1> success.txt 2> errors.txt`

7. `cp -v * ./backup/ &> report.txt`

8. `cp -v * ./backup/ &> /dev/null`

9. It searches in auth.log file for lines containing break-in case-insensitively and prints to the screen the 12th element of each line separated by space.

10. `ping -c 10 google.com | grep rtt | cut -d / -f5`

11. Single quotes are strong quotes, nothing inside them gets interpreted:

    ```bash
    $ echo '$HOSTNAME, is the name of this computer.'
    $HOSTNAME, is the name of this computer.
    $ echo "$HOSTNAME, is the name of this computer."
    ubuntu, is the name of this computer.
    ```

12. We can put it in double quotes: `greeting="Good Morning!"`

13. `echo $SECONDS` shows the number of seconds that script has been running.

14. `echo $0` inside a script shows the name of the script.

15. `echo $(($SECONDS/60))`

16. ```bash
    $ echo $f
    2
    $ echo $g
    2.50000000000000
    ```

17. The result will be *0*, indicating that the comparison is *True*.

18. Since it is comparing the string values of 20 and 100, the result is *0* or *True* meaning that *20* is a bigger string than *100*.

19. ```bash
    [[ 20 -gt 100 ]]
    echo $?
    1
    ```

20. It checks if string variable *a* is null.

21. ```bash
    name=Amir
    echo ${#name}
    4
    ```

22. ```bash
    $ name=AmirTajik
    $ d=${name: -5} && echo $d
    Tajik
    ```

23. *#* operators replaces the search term only if the string starts with it.
    *%* operator replaces the search term only if the string ends with it.

    ```bash
    letters="a b b c d d"
    echo ${letters/a/e}
    e b b c d d
    echo ${letters/#a/e}
    e b b c d d
    echo ${letters/%a/e}
    a b b c d d
    ```

24. By using double slashes: `echo ${letters//b/f}`

25. The output would be `programmer`. It finds and replaces the first *A* and every character after that, because of \*, with  *programmer*.\
If you want to repalce the names and keep the spaces, you need to be more specific with your matching expression.

26. `a=()`

27. `echo ${b[2]}`

28. Using that syntax only gives you the first element of the array so the command only displays `aa`.

29. Use @ operator to display all elements of an array.

    ```bash
    $ echo ${b[@]}
    aa bb cc ee
    ```

30. ```bash
    $ echo ${b[@]: -1}
    ee
    ```

31. Associative arrays which can only be defined in Bash 4 and above.

32. ```bash
    $ declare -A mytheme
    $ mytheme["color"]="blue"
    $ echo ${mytheme["color"]}
    blue
    ```

33. `$ > file_name`

34. `$ echo ${a_dict[@]}`

35. `$ echo ${!a_dict[@]}`

36. ```bash
    for i in "${!arr[@]}"
    do
        echo "$i: ${arr[$i]}"
    done
    ```

    > Double quotation is used around the expression which returns the keys in case some keys contain spaces in them.

37. ```bash
    for item in $@; do
        # do somthing here
    done
    ```

38. ```bash
    $ function power { echo $(( $1 ** $2 )); }
    $ power 2 3
    8
    ```

    > The semicolon is important if you are going to have a one-line function.

39. Use *$#* as in:

    ```bash
    $ function power { echo $(( $1 ** $2 )); echo "There are $# arguments."; }
    $ power 2 3 4
    8
    There are 3 arguments.
    ```
