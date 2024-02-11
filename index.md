# Lab Report 3

## Part 1:

Failure inducing input:
```
@Test
  public void testReversed() {
    int[] input1 = { 1, 2, 3 };
    assertArrayEquals(new int[] { 3, 2, 1 }, ArrayExamples.reversed(input1));
  }
```

Input that doesn't induce failure:
```
@Test
  public void testReversed2() {
    int[] input1 = {};
    assertArrayEquals(new int[] {}, ArrayExamples.reversed(input1));
  }
```
Symptom:
```
thanhlongnt@Thanh-Longs-MacBook-Pro lab3 % javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java                              
thanhlongnt@Thanh-Longs-MacBook-Pro lab3 % java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
.E.
Time: 0.005
There was 1 failure:
1) testReversed(ArrayTests)
arrays first differed at element [0]; expected:<3> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversed(ArrayTests.java:15)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<3> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 2,  Failures: 1
```

Buggy code:
Before:
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for (int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
After:
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for (int i = 0; i < arr.length; i += 1) {
      newArray[arr.length - i - 1] = arr[i];
    }
    return newArray;
  }
```
Fix Description: The innitial bugs were that `arr` was being modified instead of `newArray` (because java changes the variables that are on the left with the values on the right) and that `arr` was being returned instead of `newArray`. Simply switching the order of the modifier and returning `newArray` fixes our code and allows our test cases to pass.

## Part 2
Chosen Command: `grep`

Case insensitive search `-i`: This command line option returns files that contain a given key word. This is particularly useful when we are trying to find any sort of key word in a given text file without worrying about the formating of the text. 
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -i "hello" */*
911report/chapter-1.txt:    At 10:39, the Vice President updated the Secretary on the air threat conference: Vice President: There's been at least three instances here where we've had reports of aircraft approaching Washington-a couple were confirmed hijack. And, pursuant to the President's instructions I gave authorization for them to be taken out. Hello?
grep: government/About_LSC: Is a directory
grep: government/Alcohol_Problems: Is a directory
grep: government/Env_Prot_Agen: Is a directory
grep: government/Gen_Account_Office: Is a directory
grep: government/Media: Is a directory
grep: government/Post_Rate_Comm: Is a directory
```
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -i "guess" */*
911report/chapter-1.txt:    Right after the Pentagon was hit, NEADS learned of another possible hijacked aircraft. It was an aircraft that in fact had not been hijacked at all. After the second World Trade Center crash, Boston Center managers recognized that both aircraft were transcontinental 767 jetliners that had departed Logan Airport. Remembering the "we have some planes" remark, Boston Center guessed that Delta 1989 might also be hijacked. Boston Center called NEADS at 9:41 and identified Delta 1989, a 767 jet that had left Logan Airport for Las Vegas, as a possible hijack. NEADS warned the FAA's Cleveland Center to watch Delta 1989. The Command Center and FAA headquarters watched it too. During the course of the morning, there were multiple erroneous reports of hijacked aircraft. The report of American 11 heading south was the first; Delta 1989 was the second.
911report/chapter-10.txt:                    director had already guessed might be needed for the country as a whole.
911report/chapter-12.txt:                involve guesswork about who might be dangerous. It requires frontline border
911report/chapter-13.3.txt:                aircraft. Meanwhile, Pakistani pilots were crashing and dying." Guess how they
911report/chapter-3.txt:                only guess at how much aid Bin Ladin gave to terrorist groups, what were the main
911report/chapter-6.txt:                guessed his target was in Seattle. They did not learn about the Los Angeles airport
911report/chapter-6.txt:                the 1998 embassy bombings, a CIA desk officer guessed that "something more nefarious
911report/chapter-6.txt:                taste like an al Qaeda operation. To make a case, the CIA needed not just a guess
biomed/1471-2202-3-7.txt:        guesswork. The results of both the α 
biomed/1471-2288-3-9.txt:        uncertainty and guess at its magnitude, most do not.
biomed/1471-2288-3-9.txt:          one, rather arcane, guesstimate about how much of the
biomed/1471-2296-3-19.txt:          Additionally, we used the GUESS program, a validated
biomed/1471-2350-2-11.txt:        protein level are necessary to take some of the guesswork
biomed/1471-2458-3-20.txt:          and 12% said "can't guess." Opinions varied widely among
biomed/1472-6807-3-2.txt:          were added by using the guesscoord command in NAMD. The
biomed/gb-2002-3-12-research0081.txt:        computational analyses are synthesized into 'best guesses'
biomed/gb-2002-3-9-research0051.txt:        It is difficult to guess whether the ability of 
biomed/gb-2003-4-2-r8.txt:        investigator must make an educated guess as to which genes
biomed/gb-2003-4-2-r8.txt:        to guess ahead of time which genes these might be.
grep: government/About_LSC: Is a directory
grep: government/Alcohol_Problems: Is a directory
grep: government/Env_Prot_Agen: Is a directory
grep: government/Gen_Account_Office: Is a directory
grep: government/Media: Is a directory
grep: government/Post_Rate_Comm: Is a directory
plos/journal.pbio.0020043.txt:        because no one has even ventured a serious guess. When the phenomena were discovered, early
plos/journal.pbio.0020121.txt:        States apparently began to react badly to their captivity. At least, that was the guess of
plos/journal.pbio.0020145.txt:        journal articles they have read and want to share with me. Who would have guessed that free
plos/journal.pbio.0020147.txt:        its own dynamics that in turn influences the second locus. As one would guess, the models
plos/journal.pbio.0020147.txt:        conclusions are sparse. We guess the aim of the chapter is to illustrate that environmental
plos/journal.pbio.0020187.txt:        The escape velocity cusp is closer than you might guess. Since we are already so long
plos/journal.pbio.0020187.txt:        guess is a trebling of the remaining life span of mice of a long-lived strain that have
plos/journal.pbio.0020267.txt:        function normally,” says Aylward. “We're guessing what is missing is the experience.” To
plos/journal.pbio.0020310.txt:        and controls you're only going to be left with guesses and vague anecdotes about the
plos/pmed.0010047.txt:        second-guess the results of field trials. This is partly because we do not have any good
plos/pmed.0010056.txt:        similar to the problem faced by subsidy proposals: guessing private-sector R&D costs.
plos/pmed.0010056.txt:        price—and guessing wrong is likely to be expensive. Second, Virtual Pharma's development
plos/pmed.0020035.txt:        There is another reason why a best-guess timeline is essential: realistic expectations
```

Displaying the count of number of matches `-c`: This command returns the number of matches a file contains for a given key word. This is useful when we are scanning for files containing the key words, without having the entire text file as the output. 
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -c "guess" 911report/*
911report/chapter-1.txt:1
911report/chapter-10.txt:1
911report/chapter-11.txt:0
911report/chapter-12.txt:1
911report/chapter-13.1.txt:0
911report/chapter-13.2.txt:0
911report/chapter-13.3.txt:0
911report/chapter-13.4.txt:0
911report/chapter-13.5.txt:0
911report/chapter-2.txt:0
911report/chapter-3.txt:1
911report/chapter-5.txt:0
911report/chapter-6.txt:3
911report/chapter-7.txt:0
911report/chapter-8.txt:0
911report/chapter-9.txt:0
911report/preface.txt:0
```
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -c "hello" 911report/* 
911report/chapter-1.txt:0
911report/chapter-10.txt:0
911report/chapter-11.txt:0
911report/chapter-12.txt:0
911report/chapter-13.1.txt:0
911report/chapter-13.2.txt:0
911report/chapter-13.3.txt:0
911report/chapter-13.4.txt:0
911report/chapter-13.5.txt:0
911report/chapter-2.txt:0
911report/chapter-3.txt:0
911report/chapter-5.txt:0
911report/chapter-6.txt:0
911report/chapter-7.txt:0
911report/chapter-8.txt:0
911report/chapter-9.txt:0
911report/preface.txt:0
```

Display the file names that matches the pattern `-l`: This command returns the files that contain the input word. It is useful when trying to locate files that contain such key word without additional information.
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -l "code" 911report/*
911report/chapter-1.txt
911report/chapter-10.txt
911report/chapter-13.2.txt
911report/chapter-13.4.txt
911report/chapter-13.5.txt
911report/chapter-2.txt
911report/chapter-3.txt
911report/chapter-5.txt
911report/chapter-7.txt
```
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -l "hello" 911report/*
thanhlongnt@Thanh-Longs-MacBook-Pro technical %
```

Checking for the whole words in a file `w`: This command returns files that contain the specific key word with regard to formating. It is useful when we are trying to look for key words that are not part of a substring.
```
911report/chapter-1.txt:    FAA guidance to controllers on hijack procedures assumed that the aircraft pilot would notify the controller via radio or by"squawking"a transponder code of "7500"-the universal code for a hijack in progress. Controllers would notify their supervisors, who in turn would inform management all the way up to FAA headquarters in Washington. Headquarters had a hijack coordinator, who was the director of the FAA Office of Civil Aviation Security or his or her designate.
911report/chapter-1.txt:    Minutes later, United 175 turned southwest without clearance from air traffic control. At 8:47, seconds after the impact of American 11, United 175's transponder code changed, and then changed again. These changes were not noticed for several minutes, however, because the same New York Center controller was assigned to both American 11 and United 175. The controller knew American 11 was hijacked; he was focused on searching for it after the aircraft disappeared at 8:46.
911report/chapter-10.txt:                Originally titled "Infinite Justice," the operation's code word was changed-to avoid
911report/chapter-13.2.txt:                transponder signal was turned off at 8:21; on United 175, the code was changed at
911report/chapter-13.4.txt:                money, the code, and perhaps the identity of the recipient. The ultimate recipient
911report/chapter-13.5.txt:                by a code, and individuals' ranks or units are disclosed only in a broad manner.
911report/chapter-13.5.txt:                already been made not to return to Washington, a reported threat to "Angel"-the code
911report/chapter-13.5.txt:                discuss the adoption of a standard requiring a digital code for all names that need
911report/chapter-2.txt:                fundamental source. A third key element is the Sharia, the code of law derived from
911report/chapter-2.txt:            Islam is both a faith and a code of conduct for all aspects of life. For many
911report/chapter-3.txt:                down" joined "Desert One" as a symbol among Americans in uniform, code phrases used
911report/chapter-3.txt:                were given the code name Operation Infinite Resolve.
911report/chapter-5.txt:                read phone books, interpret airline timetables, use the Internet, use code words in
911report/chapter-5.txt:                apparently, was simply a code; a group of Afghans from the office promptly escorted
911report/chapter-7.txt:                to KSM, who then trained Hanjour for a few days in the use of code words.
911report/chapter-7.txt:                Zacarias Moussaoui. Binalshibh soon contacted KSM and, using code words, reported
911report/chapter-7.txt:                mid-August. According to Binalshibh, Atta used a riddle to convey the date in code-a
```
```
thanhlongnt@Thanh-Longs-MacBook-Pro technical % grep -w "hello" 911report/*
thanhlongnt@Thanh-Longs-MacBook-Pro technical %
```


