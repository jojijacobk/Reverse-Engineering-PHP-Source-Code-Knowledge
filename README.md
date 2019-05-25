   * [Reverse Engineering PHP Source Code](README.md#reverse-engineering-php-source-code)
   * [Doxygen](README.md#doxygen)
   * [phpCallGraph](README.md#phpcallgraph)
   * [Xdebug](README.md#xdebug)
      * [Function Trace](README.md#function-trace)
      * [Profiler](README.md#profiler)
      * [PHP.ini Settings for Xdebug Function Trace &amp; Profiler](README.md#phpini-settings-for-xdebug-function-trace--profiler)
      * [Cachegrind Output → Sequence Diagrams](README.md#cachegrind-output-sequence-diagrams)


# Reverse Engineering PHP Source Code

When you stumble up on a large source code which you want to work with,
the first step you need to do will be to understand the structure of
code. There are several tools to perform reverse engineering such as
static code structure analysis, static document generator, function
trace, execution call graph etc.

# Doxygen

Doxygen is the de facto standard tool for generating documentation from
annotated C++ sources, but it also supports other popular programming
languages such as C, Objective-C, C\#, PHP, Java, Python etc.

[http://www.stack.nl/\~dimitri/doxygen/index.html](index)

# phpCallGraph

phpCallGraph is a tool to generate static call graphs for PHP source
code. Such a graph visualizes the call dependencies among methods or
functions of an application. Arrows represent calls from one method to
another method. Classes are drawn as rectangles containing the
respective methods. The graphs can be leveraged to gain a better
understanding of large PHP applications or even to debunk design
flaws in them.

<http://phpcallgraph.sourceforge.net>

# Xdebug

## Function Trace

Xdebug allows you to log all function calls, including parameters and
return values to a file in different formats. Intellij can read and
analyse the xdebug trace output files.

<https://xdebug.org/docs/execution_trace>

## Profiler

Profiler generates a file in cachegrind format, which can be viewed by
**kcachegrind** or **qcachegrind** or **webgrind**. It has a call graph
representing the function invocations for a particular request. This can
also be read and analysed by Intellij to show Call Tree.

## PHP.ini Settings for Xdebug Function Trace & Profiler

``` java
[xdebug]
; Enable xdebug
zend_extension=/usr/lib64/php/modules/xdebug.so
xdebug.remote_log="/var/log/xdebug.log"
xdebug.remote_enable=1
xdebug.remote_host=10.0.2.2
xdebug.remote_port=9000
xdebug.remote_autostart=0
xdebug.remote_handler="dbgp"
xdebug.remote_mode=req
;xdebug.remote_connect_back=1

; Enable Function Traces
;xdebug.collect_params=4
;xdebug.collect_return=1
xdebug.trace_output_dir="/home/jojijacobk/XdebugAnalysis"
xdebug.trace_output_name="trace.%s"
xdebug.auto_trace=0

; Enable Profiler
xdebug.profiler_enable=1
xdebug.profiler_output_dir="/home/jojijacobk/XdebugAnalysis"
```

## Cachegrind Output → Sequence Diagrams

1.  **Generate Cachegrind Files**. Enable Xdebug Profiler and execute
    the source code you need to understand. This will generate
    cachegrind output files.
2.  **Load Cachegrind Files into Intellij** → Analyze Xdebug Profiler
    Snapshot. This will show you Call Tree. Read Call Tree from bottom
    up to understand code execution tree.
3.  **Load Cachegrind Files to visualization tools** → Webgrind or
    Qcachegrind or Kcachegrind. This will show you a graphical view of
    the code execution tree.
4.  **Load Cachegrind Files to PlantUML** →  Sequence Diagram generator.
    This will show you sequence diagrammatic view of code execution
    tree. And, you could also fine tune the plantuml to modify sequence
    diagram as needed.
