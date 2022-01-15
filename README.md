# Scala & Play Hello World Investigation Exercises

In this exercise you will make some small changes to a sample codebase from the
HMRC github organisation. Your goal is to gain understanding of how this
codebase functions, and in the process some knowledge that you can generalise to
other codebases.

In your job, you will encounter a great deal of complexity — more than you could
learn in a couple of weeks or even a couple of months. What will set you up for
success is your research, analysis, and problem-solving skills. 

Work carefully through these exercises, and pay close attention to the code to
understand what is going on before diving in with a change.

To clone the project:

```shell
; git clone git@github.com:hmrc/api-example-microservice.git
; git checkout 11c5bf # This gets you to the right point in history
```


## Exercise 1: Get the codebase running

To do this you will need to make sure you are using JDK 8, 11, or 15.

In IntelliJ you should change this in 'File -> Project Structure -> Project SDK'.

Then you can do the following to set up your terminal:

```shell
; brew install openjdk@11
; echo 'export PATH="/usr/local/opt/openjdk@11/bin:$PATH"' >> ~/.zshrc
# Then open a new terminal to refresh

# Run the tests
; ./run_all_tests.sh
# You should see all the tests run successfully
# You can safely ignore errors related to dependency report for now

# Run the server
; ./run_local.sh
# You should see 'listening for HTTP on /0:0:0:0:0:0:0:0:9601'

# And in a new terminal, make a request.
# Note that the 'Accept' header must be exactly like this.
; curl http://localhost:9601/world -H "Accept: application/vnd.hmrc.1.0+json"
{"message":"Hello World"}
```

If you encounter errors it is probably your Java version. Contact a coach for
help.

## Exercise 2: Diagram the request

Diagram out the request you made above using cURL. Include these aspects:

* How does the client (cURL) interact with the server?
* How does the server serve the request?
* Where does the text come from?

You may wish to use [Draw.io](http://draw.io/) or
[Excalidraw](http://excalidraw.com/).

## Exercise 3: Add a new route

Add a new route so that this request works as follows:

```shell
; curl http://localhost:9601/johnny -H "Accept: application/vnd.hmrc.1.0+json"
{"message":"Hello Johnny!"}
```

In your job you will be expected to include tests, so you should include tests
here. 

For this, look at `component/resources/features/`. You may be surprised by what
you find! To read more about this technology, visit
[Cucumber.io](https://cucumber.io). To see the code behind the features, see
`component/scala/steps`.

## Exercise 4: Add a new data type

Amend the code so that these requests work:

```shell
; curl http://localhost:9601/world -H "Accept: application/vnd.hmrc.1.0+text"
Hello World
; curl http://localhost:9601/application -H "Accept: application/vnd.hmrc.1.0+text"
Hello Application
; curl http://localhost:9601/user -H "Accept: application/vnd.hmrc.1.0+text"
Hello User
; curl http://localhost:9601/johnny -H "Accept: application/vnd.hmrc.1.0+text"
Hello Johnny!
```

Include test.

For this assignment, you will need to work out how the application processes the
`Accept` request and how the controller decides what data type to send back.
