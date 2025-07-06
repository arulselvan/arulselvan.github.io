---
author: Arul Selvan
category:
  - software-development
date: "2023-10-30T23:56:17+00:00"
draft: "true"
guid: http://arulselvan.net/?p=424
title: Choosing a language for MicroServices
url: /

---
Today one of the challenging is choosing right language for new project requirement, here just shared my comparative study between C#, Java and Go.

Nothing to boast any of the languages, everything has positive and negative, below described how I did a comparative study for my requirements

Okay, What is my requirements ?

- Rest API
- RealTime Events SSE/WebSocket
- Consuming messages from one of the queues/streams like Kafka or ZeroMQ
- Working with MySQL Database and Elasticsearch Search Engine
- DevOps (Dockerization and CI/CD support)
- Readability and maintainability of code

Before going into my requirement study, let see some high level overview about each language and its compilation and execution flow

C#

C# programs run on the .NET Framework. .NET has a virtual machine called common language runtime (CLR). CLR is responsible for creating executing and development environment for all the .net framework supported languages.

Source code written in C# is compiled into an intermediate language(IL). IL code and resources stored on a disk in executable file called an assembly, typically with an extension .dll or exe.

When the C# program is executed, the assembly is loaded into the CLR, which might take various actions. The CLR performs Just-In-Time (JIT) compilation to convert the IL code to native machine instructions.

Below Diagram described the same

![](/wp-content/uploads/2020/05/c-sharp-overview.png)

Java

Java programs run on the Java runtime environment(JRE). JRE has virtual machine called Java Virtual Machine(JVM). JVM is responsible for creating executing and development environment for Java

Source code written in Java is compiled into Byte code, The most common form of output from a Java compiler is Java class files

The JVM loads the class files and just in time compiles it to machine code

Go

#### Rest API and RealTime Events SSE
