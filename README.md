## 95-702 Distributed Systems Lab 1

You are not required to submit your work for this lab. But, to make progress on the projects and to perform well on the exams, it is essential that you complete it.

If you have difficulty or questions, post your questions to Piazza or see a TA or an instructor during office hours or during the class time set aside for lab work.

### Objectives:

In this lab, you will do four things: First, you will install the Open JDK, IntelliJ, and TomEE Plus. These tools will be used throughout much of the course. Second, in order to get familiar with the IDE, you will complete some small programming exercises. Third, to get some hands on experience with distributed consensus, you will complete some exercises using the Raft simulator. And fourth, you will work with cryptographic hashes. The computing of these hashes will come up several times in our course.

Answers to all of the exercises appear at the bottom of this lab.

For those using a Windows operating system, you will need to use a "Pro" version of Windows (not a "Home" version).

### Part 1. Installation of Open JDK

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

### Part 2. Installation of IntelliJ IDEA Ultimate

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

### Part 3. Installation of TomEE+

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
11. Project SDK: 16
12. Next and select Version: Jakarta EE 9 on the top left.
13. Select the servlet box and then Finish.

**The Project Window**

1. Under src/main/java should be a package named ds.helloworld containing HelloServlet.java
2. Under webapp you should find index.jsp.
3. Under webapp/WEB-INF you should find web.xml.
4. The file pom.xml is near the root of the hierarchy.

**Steps 5 and 6 are optional if you did not select Jakarta in step 12.**

5. Change your pom.xml by replacing

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
6. The jakarta.platform may be in red. In any case, go to View/Tool Windows/Maven/click circular arrow icon "reload all Maven projects". Close that window by clicking the minus sign.

7. Choose File/Project Structure/  

   Project Name: HelloWorld  

   Project: Project SDK 16  

   Platform Settings: SDK's choose 16 (Records, patterns...  

   Select OK.

8. Select Edit Configurations. The "Edit Configurations" is found by clicking the down arrow just to the right of TomEE 10.0.41
in the top right of the IDE.
9. Change the URL. The URL should read http://localhost:8080/HelloWorld-1.0-SNAPSHOT/

10. Select Apply and OK.

11. To run your web application, click the green triangle.

12. A test browser should run with Hello World.

13. In addition, you should also be able to select and run your servlet.
***
**Exercise 3**

Modify your JSP file so that the browser displays the link
with the label "Compute Hash" instead of "Hello World".
***

**Exercise 4**

Modify the servlet code so that, when visited, it displays
the SHA-256 Hex string of "Hello World" on the browser.

***

### Part 4. Working with Raft

1. [Visit the Raft Simulator](https://raft.github.io/raftscope/index.html) and experiment with it.

2. Set the bottom rail to 1/100x. This rail controls the speed of the simulator.

3. Set the upper rail to the far left. This is time 0. The simulator allows you to pause execution of the distributed algorithm and go back in time to time 0.

4. One of the followers will time out and request votes.
A leader will be selected. Let's call the first leader L.

5. Click the leader L and make a request to it.

***
**Exercise 5**

Explain why the request is not committed on the peers (with dark edges surrounding the term) until after the leader visits twice - once with the request and then a follow up confirmation.

***


Make many requests from the same leader. Perform more than 11 requests to leader L and watch the logs on each peer grow. Experiment with the top slider. Drag it left to go back in time.  

6.	Refresh the simulator. Experiment and get the Raft simulator to show the following replicated logs. Note, the final server need not be S1. The only requirement is that each log is identical to the one shown in this screen copy:

<img src="https://github.com/CMU-Heinz-95702/Lab1-InstallationAndRaft/blob/master/images/Figure1.png" alt="Experiment with Raft" width="400" height="400"/>  


7. Working with a fresh copy of the Raft simulator, do the following:

- a. Send two requests from the leader to all followers.

- b. Stop one of the followers.

- c. Send four requests from the leader to the remaining followers.

- d. Resume the stopped follower.
***
**Exercise 6**
Explain what happened and why.
***
8. Working with a fresh copy of the Raft simulator, do the following:

- a. Wait until a single leader is established.

- b. Stop three of the four followers.

- c. Send three requests from the leader, one after the other.

***
**Exercise 7**
Explain what happened and why. Also, explain what happens if the three followers are started back up.
***

### Part 5. Working with hashes

In the slides on Nakamoto consensus, see
[1_Blockchain_Raft_and_Nakamoto.pdf](https://canvas.cmu.edu/courses/19194/files/5122183/download?wrap=1),
there is a quiz question that asks:

Quiz: Which of the blocks on the right can be the next block in the chain of length 2? Format: Nonce,Difficulty,id,Tx1,Tx2,HashPointer

***
**Exercise 8**
[Use the SHA256 calculator that you used before](https://emn178.github.io/online-tools/sha256.html) to answer the quiz question on the slides.

Note: There are no newlines or return characters in the correct answer.
***

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

Place the string "Compute hash" in the html anchor element.

**Exercise 4 Answer**

```
package edu.cmu.andrew.hashofhelloworld;

import java.io.*;

import jakarta.servlet.http.*;
import jakarta.servlet.annotation.*;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

@WebServlet(name = "helloServlet", value = "/hello-servlet")
public class HelloServlet extends HttpServlet {
    private String message;

    public void init() {
        message = "The SHA256 Hash of Hello World is ";
    }

    public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        response.setContentType("text/html");

        try {
            // Access MessageDigest class for SHA-265
            MessageDigest md = MessageDigest.getInstance("SHA-256");
            // Compte the digest
            md.update("Hello World".getBytes());
            String hash = bytesToHex(md.digest());
            // echo to console
            System.out.println(hash);
            // get a print writer from the the response object
            PrintWriter out = response.getWriter();
            // send an html document to caller
            out.println("<html><body>");
            // compute digest, convert to hex, send back to caller
            out.println("<h1>" + message + hash + "</h1>");
            out.println("</body></html>");
        }
        catch(NoSuchAlgorithmException e) {
            System.out.println("No SHA-256 available" + e);
        }
    }

    public void destroy() {
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
```

**Exercise 5 Answer**
None of the nodes commit the request until a majority of nodes have voted to commit the request. So, simply receiving the request and responding with a vote is not enough. The peer must wait until the server counts the votes and affirms that a majority says to commit.

**Exercise 6 Answer**
The additional four requests were not replicated to the stopped follower. But, when the follower came back online, the algorithm brought the follower up to date with the correct replica.

**Exercise 7 Answer**
The three request are being held by two machine as tentative and not committed. There is no majority support for these requests.
When the three followers are resumed, they are told of the three requests and the entire cluster comes into consensus.

**Exercise 8 Answer**
109346,5,19,Pink,Orange,002fdb16086d97e03613fa0caa87b280eca956216e61a35400408bdd3a449e45

When hashed with SHA-256, has five, leftmost zeroes.
