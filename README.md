CAPS.Net
========

Command-line Arguments Parser Simulator for .Net (C.A.P.S (dot Net))

The library to assist you in subcutaneous testing of Console Applications with command line arguments.

The command-line takes a string. But your application takes a list of strings.
Sometimes you just want to provide one string and not the list, like your shell scripts do.
This is where CAPS.Net comes in. We simulate the argument splitting so that you don't have to!
This is great for testing console applications using `Program.Main(args)` or `new Program(args)` entry points
and get test coverage over your command-line argument parsing without having to work out how to split the args yourself.
(Especially when there are some interesting edge-cases to worry about.)

Usages
------

``` cs
public static MyAppRunResults RunMyApp(string arguments, TestDependency aDependency = null)
{
    string[] appArgs = ArgsParser.Parse(arguments);
    var exitCode = new Program(aDependency ?? new TestDependency()).Run(appArgs);

    foreach (var line in testConsole.StandardOut)
    {
        Console.WriteLine(line);
    }

    return new MyAppRunResults
    {
        StandardError = testConsole.Errors,
        StandardOutput = testConsole.StandardOut,
        ExitCode = exitCode
    };
}


[Fact]
public void NoArguments_ExitCodeNotSuccess()
{
    var results = RunMyApp(string.Empty);

    Assert.NotEqual(0, results.ExitCode);
}
```