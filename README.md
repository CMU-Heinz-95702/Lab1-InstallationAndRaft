## 95-702 Distributed Systems Lab 1

You are not required to submit your work for this lab. But, to make progress on the projects and to perform well on the exams, it is essential that you complete it.

If you have difficulty or questions, post your questions to Piazza or see a TA or an instructor during office hours or during the class time set aside for lab work.

### Objectives:

In this lab, you will install Open JDK, IntelliJ, and TomEE Plus. These tools will be used throughout much of the course. You will also solve some Raft puzzles and answer questions about proof of work and SHA256.

Answers to the questions appear at the bottom of this lab.

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

Establish your student credentials with JetBrains. [Download the free version of IntelliJ for educational use](https://www.jetbrains.com/student/).

The "Ultimate" edition is the one we will use.
Download and install the latest IntelliJ IDEA Ultimate.

When you create a new project, you should be able to select your new JDK.

**Question 1**

Write a program that imports the MessageDigest class from the java.security package. Use the MessageDigest class to compute and display the SHA-256 digest of "Hello World".

**Part 3. Installation of TomEE+**

[Download TOMEE ](http://tomee.apache.org/download-ng.html)
and download the TomEE 9.x.x (e.g 8.0.4) version of **TomEE Plus**
(Note: "Plus", not "Plume".)

Copy the TomEE directory to an appropriate directory on your file
system. The directory path should contain no spaces. Do not change the
name of the TomEE Plus directory.

1.  Open IntelliJ and create a new project.

2.  Under Java/ Java EE /select Web Application

3.  Select Next and name your project TestWebApp

4.  Right click src and create a new servlet

5.  Give it the name TestServlet in the package
    edu.cmu.andrew.yourAndrewID

6.  Select OK

7.  In the web.xml file, after the servlet element, create a servlet
    mapping element as shown here:

\<servlet-mapping>

\<servlet-name>TestServlet\</servlet-name>

\<url-pattern>/\*\</url-pattern>

\</servlet-mapping>

8.  Open the TestServlet in the src directory. Within the doGet method,
    add this line of code:

response.getWriter().append(\"Hello from TestServlet \");

9.  Select Run/Edit Configurations/+/TomEE Server/Local

10. Name the server MyTomEE

11. Select Configure

12. In TomEE text box, select the folder on the far right.

13. Select open after browsing to the apache-tomee-plus directory.
    Select OK.

14. Select Deployment and click Fix in the bottom right and then OK.

15. Select File/Project Structure/Project Settings/Libraries/+/Java

16. Navigate to TomEE plus directory and select lib/apply/OK

17. Select the green Run triangle.

> 18\. A browser runs and you should see Hello from TestServlet.

Show your TA your browser visiting the TestServlet.

This is the checkmark for this lab.

While testing, leave the following settings alone. You should just work
from

the defaults provided.

You can set the URL with:

Run/Edit Configurations/Deployment/Application Context

The test browser visits the location specified at:

Run/Edit Configurations/Server/Open browser/URL

**Part 4. Working with Raft**

1)  Visit
    [[https://raft.github.io/raftscope/index.html]{.ul}](https://raft.github.io/raftscope/index.html)
    and play with the Raft simulator.

2)  Show your TA that you were able to get the Raft simulator to show
    the following replicated logs. Note, the final server need not be
    S1. The only requirement is that each log is identical to the one
    shown in Figure 1.

> ![](media/image1.png){width="3.165790682414698in"
> height="2.7038899825021874in"}
>
> Figure 1: Answer to question 7

3)  Working with a fresh copy of the Raft simulator, do the following:

```{=html}
<!-- -->
```
A.  Send two requests from the leader to all followers.

B.  Stop one of the followers.

C.  Send four requests from the leader to the remaining followers.

D.  Resume the stopped follower. Explain to your TA what happened.

4)  Working with a fresh copy of the Raft simulator, do the following:

```{=html}
<!-- -->
```
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

**Answer to question 1**

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
