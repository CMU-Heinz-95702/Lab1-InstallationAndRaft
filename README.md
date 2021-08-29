## 95-702 Distributed Systems Lab 1

You are not required to submit your work for this lab. But, to make progress on the projects and to perform well on the exams, it is essential that you complete it.

If you have difficulty or questions, post your questions to Piazza or see a TA or an instructor during office hours or during the class time set aside for lab work.

### Objectives:

In this lab, you will do two things: (1) install Open JDK, IntelliJ, and TomEE Plus. These tools will be used throughout much of the course. And (2) you will complete some small programming exercises and some exercises using the Raft simulator.

Answers to the exercises appear at the bottom of this lab.

For those using a Windows operating system, you will need to use a "Pro" version of Windows (not a "Home" version).

**Part 1. Installation of Open JDK**

When downloading the JDK, be sure to choose OpenJDK 16.

[Download the current version of Java](https://adoptium.net/).
Set your JAVA_HOME environment variable.

On a MAC, JAVA_HOME is set within the .bash_profile of your home directory.
```
export JAVA_HOME=/Library/Java/JavaVirtualMachines/temurin-16.jdk/Contents/Home

```

On a Windows machine, add a JAVA_HOME environment variable. The value of this variable is the directory path where the JDK was installed.

To test your setup, open the command line shell. From the command line, javac -version and java -version should both
report the version number as 16.X.X. Be sure that the versions of java and javac are identical. On my machine, I see 16.0.2 for both java and javac.

**Part 2. Installation of IntelliJ IDEA Ultimate**

Establish your student credentials with JetBrains and [download the free version of IntelliJ for educational use](https://www.jetbrains.com/student/).

The "Ultimate" edition is the one we will use.
Download and install the latest IntelliJ IDEA Ultimate.

Create a simple Java project:
1. File/New Project/Project SDK Browse to version 16
2. Next/Check Create Project From Template
3. Next/Name is Lab1Project/Base Project is edu.cmu.andrew.YOURID
4. Finish
5. Enter some Java source and use the green triangle to compile and execute.

***
**Exercise 1**

Write a program that imports the MessageDigest class from the java.security package. Use the MessageDigest class to compute and display the SHA-256 digest of "Hello World". (A possible answer is below.)
***

**Exercise 2**

[Visit this SHA256 calculator](https://emn178.github.io/online-tools/sha256.html).

Do you get the same answer form the calculator that you got from the Java program?
***

**Part 3. Installation of TomEE+**

[Visit Apache TOMEE ](http://tomee.apache.org/download-ng.html)
and download the TomEE 9 version of **TomEE Plus**
(Note: "Plus", not "Plume".) Later, you may see TomEE 10 in the IDE - even though you have installed 9. No worries.

Copy the TomEE directory to an appropriate directory on your file
system. The directory path should contain no spaces. Do not change the name of the TomEE Plus directory.

**Configure a "Hello World" web site:**

1. Choose New Project.
2. Choose Java Enterprise.
3. Name: HelloWorld
4. Change the location if appropriate.
5. Project Template: Select Web Application
6. Application server: Click new
7. From TomEE Server, browse to your TomEE home directory and select OK. Mine looks like this: /Applications/apache-tomee-plus-9.0.0-M7
8. Java, Maven, JUNit should be checked.
9. Set your group to ds
10. Your artifact should already be set to HelloWorld.
10. Project SDK: 16
11. Next and select Version: Jakarta EE 9 on the top left.
12. Select the servlet box and then Finish.

**The Project Window**

1. Under src/main/java should be a package named ds.helloworld containing HelloServlet.java
2. Under webapp you should find index.jsp.
3. Under webapp/WEB-INF you should find web.xml.
4. Change your pom.xml by replacing
```
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>
```
        with this:
```
        <dependency>
            <groupId>jakarta.platform</groupId>
            <artifactId>jakarta.jakartaee-api</artifactId>
            <version>9.0.0</version>
            <scope>provided</scope>
        </dependency>
```
5. The jakarta.platform may be in red. In any case, go to View/Tool Windows/Maven/click circular arrow icon "reload all Maven projects". Close that window by clicking the minus sign.

6. Choose File/Project Structure/
   Name: HelloWorld
   Project: Project SDK 16
   Platform Settings: SDK's choose 16
   Select OK.

7. Select Edit Configurartions. The Edit Configurations is found by clicking the down arrow just to the right of TomEE 10.0.41
in the top right of the IDE.
8. Change the URL. The URL should read http://localhost:8080/HelloWorld-1.0-SNAPSHOT/
9. Select the green Run triangle.

10. A test browser should run with Hello World.

11. In addition, you should also be able to select and run your servlet.

**Exercise 3**

Modify your JSP file so that the browser displays the string
"Front Page" instead of "Hello World".

**Exercise 4**

Modify the servlet code so that, when visited, it displays
the SHA-256 Hex string of "Hello World" on the browser.


**Part 4. Working with Raft**

1) [Visit the Raft Simulator](https://raft.github.io/raftscope/index.html) and experiment with it.

Set the bottom rail to 1/100x. This rail controls the speed of the simulator.

Set the upper rail to the far left. This is time 0. The simulator allows you to pause execution of the distributed algorithm and go back in time to time 0.

One of the followers will time out and request votes.
A leader will be selected. Let's call the first leader L.

Click the leader L and make a request to it.

***
**Exercise 3**

Explain why the request is not committed on the peers (with dark edges surrounding the term) until after the the leader visits twice - once with the request and then a follow up confirmation.

***


Make many requests from the same leader. How many requests
are actually shown in the display? (barely see request 11).

2)	Experiment and get the Raft simulator to show the following replicated logs. Note, the final server need not be S1. The only requirement is that each log is identical to the one shown in Figure 1.

<img src="https://github.com/CMU-Heinz-95702/Lab1-InstallationAndRaft/blob/master/images/Figure1.png" alt="Experiment with Raft" width="400" height="400"/>


3)  Working with a fresh copy of the Raft simulator, do the following:

A.  Send two requests from the leader to all followers.

B.  Stop one of the followers.

C.  Send four requests from the leader to the remaining followers.

D.  Resume the stopped follower.

4)  Working with a fresh copy of the Raft simulator, do the following:

A.  Wait until a single leader is established.

B.  Stop three of the four followers.

C.  Send three requests from the leader, one after the other.

D.  Explain to your TA what happened.

**Part 5. Working with hashes**

In the slides on Nakamoto consensus, see
[1_Blockchain_Raft_and_Nakamoto.pdf](https://canvas.cmu.edu/courses/19194/files/5122183/download?wrap=1),
there is a quiz question that asks:

Quiz: Which of the blocks on the right can be\
the next block in the chain of length 2?\
Format: Nonce, Difficulty, id, Tx1, Tx2, HashPointer

Use the SHA256 calculator at this URL:

<https://www.xorbin.com/tools/sha256-hash-calculator>,

Show your TA, by referring to the hash, that you have chosen the correct
answer.

Note: There are no newlines or return characters in the correct answer.

## Answers to Exercises

**Exercise 1 Answer**


```
package edu.cmu.andrew.yourID;

import java.security.MessageDigest;

public class Main {

    public static void main(String[] args) throws Exception {

        System.out.println("Hello World");
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        md.update("Hello World".getBytes());
        System.out.println(bytesToHex(md.digest()));
    }

    // Code from stack overflow
    // https://stackoverflow.com/questions/9655181/how-to-convert-a-byte-array-to-a-hex-string-in-java
    // Returns a hex string given an array of bytes
    private static final char[] HEX_ARRAY = "0123456789ABCDEF".toCharArray();
    public static String bytesToHex(byte[] bytes) {
        char[] hexChars = new char[bytes.length * 2];
        for (int j = 0; j < bytes.length; j++) {
            int v = bytes[j] & 0xFF;
            hexChars[j * 2] = HEX_ARRAY[v >>> 4];
            hexChars[j * 2 + 1] = HEX_ARRAY[v & 0x0F];
        }
        return new String(hexChars);
    }

}
/*  Output
    Hello World
    A591A6D40BF420404A011733CFB7B190D62C65BF0BCDA32B57B277D9AD9F146E
*/
```
**Exercise 2 Answer**

Yes. Any correct SHA-256 calculator will provide the same value as that generated by the Java program.

**Exercise 3 Answer**

Place the string "Front Page" after the percent equals.

**Exercise 4 Answer**

TBD


**Exercise 5 Answer**
Answer: None of the nodes commit the request until a majority of nodes have voted to commit the request. So, simply receiving the request and responding with a vote is not enough. The peer must wait until the server counts the votes and affirms that a majority says to commit.
