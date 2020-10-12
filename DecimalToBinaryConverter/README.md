## Not your usual decimal to binary converter

<p float="center">
  <img src="output for notYourUsualDecToBin.png" />
</p>

### Explanation

Original one-liner
    
    (_$=($,_=[]+[])=>$?_$($>>+!![],($&+!![])+_):_)(420);

After breathing

    ( _$ = ( $,_=[]+[] ) => $ ? _$ ($>>+!![],($&+!![])+_) : _ )(420);

    ( _$ = ( $ , _ = []+[] ) => $ ? _$ ( $ >> +!![] , ($&+!![]) +_ ) : _ )(420);

    ( _$ = ( $ , _ = []+[] ) => $ ? _$ ( $ >> +!![] , ( $ & +!![] ) + _ ) : _ )(420);

---

Renaming ***_$*** with ***dec2bin*** , ***$*** with ***dec*** , ***_*** with ***bin***

    ( dec2bin = ( dec , bin = []+[] ) => dec ? dec2bin ( dec >> +!![] , ( dec & +!![] ) + bin ) : bin )(420);

Removing self execution

    dec2bin = ( dec , bin = []+[] ) => dec ? dec2bin ( dec >> +!![] , ( dec & +!![] ) + bin ) : bin;

    dec2bin(420);

Focusing on the function only!

Taking out arrow function and removing ternary operator

    function dec2bin ( dec , bin = []+[] ) {
        if (dec) {
            return dec2bin ( dec >> +!![] , ( dec & +!![] ) + bin )
        } else {
            return bin;
        }
    }

---


    ![]     -> false
    !![]    -> true

    + operator is used to convert bool -> value

    +![]    -> 0
    +!![]   -> 1

    Concatting 2 empty [] will result in ""

Cleaning!

    function dec2bin ( dec , bin = []+[] ) {
        if (dec) {
            return dec2bin ( dec >> 1 , ( dec & 1 ) + bin )
        } else {
            return bin;
        }
    }

---

*Halving the dec value each iteration and adds the remainder to the beginning*

Sample run of the recursion 

    dec2bin ( 4 , bin = "")
        dec2bin( 2 , "0" + "")
            dec2bin( 1 , "0" + "0" + "")
                dec2bin( 0 , "1" + "0" + "0" + "")

    // returns "100" when dec is "4"


    dec2bin( 3, bin="")
        dec2bin( 1 , "1" + "")
            dec2bin( 0, "1" + "1" + "")

    // returns "11" when dec is "3"