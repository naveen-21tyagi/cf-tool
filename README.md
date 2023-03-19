# Codeforces Tool

Codeforces Tool is a command-line interface tool for [Codeforces](https://codeforces.com).

It's fast, small, cross-platform and powerful.

[Usage](#usage)

## Features

* Support Contests, Gym, Groups and acmsguru.
* Support all programming languages in Codeforces.
* Submit codes.
* Watch submissions' status dynamically.
* Fetch problems' samples.
* Compile and test locally.
* Clone all codes of someone.
* Generate codes from the specified template (including timestamp, author, etc.)
* List problems' stats of one contest.
* Use default web browser to open problems' pages, standings' page, etc.
* Setup a network proxy. Setup a mirror host.
* Colorful CLI.

Pull requests are always welcome.

![](./assets/readme_1.gif)

## Usage

Let's simulate a competition.

 `cf race 1136` or `cf race https://codeforces.com/contest/1136`

To start competing the contest 1136!

If the contest has not started yet, `cf` will count down. If the contest have started or the countdown ends, `cf` will use the default browser to open dashboard's page and problems' page, and fetch all samples to the local.

 `cd ./cf/contest/1136/a` (May be different from this, please notice the message on your screen)

Enter the directory of problem A, the directory should contain all samples of the problem.

 `cf gen` 

Generate a code with the default template. The filename of the code is problem id by default.

 `vim a.cpp` 

Use Vim to write the code (It depends on yourself).

 `cf test` 

Compile and test all samples.

 `cf submit` 

Submit the code.

 `cf list` 

List problems' stats of the contest.

 `cf stand` 

Open the standings' page of the contest.

```plain
You should run "cf config" to configure your handle, password and code
templates at first.

If you want to compete, the best command is "cf race".

Usage:
  cf config
  cf submit [-f <file>] [<specifier>...]
  cf list [<specifier>...]
  cf parse [<specifier>...]
  cf gen [<alias>]
  cf test [<file>]
  cf watch [all] [<specifier>...]
  cf open [<specifier>...]
  cf stand [<specifier>...]
  cf sid [<specifier>...]
  cf race [<specifier>...]
  cf pull [ac] [<specifier>...]
  cf clone [ac] [<handle>]
  cf upgrade

Options:
  -h --help            Show this screen.
  --version            Show version.
  -f <file>, --file <file>, <file>
                       Path to file. E.g. "a.cpp", "./temp/a.cpp"
  <specifier>          Any useful text. E.g.
                       "https://codeforces.com/contest/100",
                       "https://codeforces.com/contest/180/problem/A",
                       "https://codeforces.com/group/Cw4JRyRGXR/contest/269760",
                       "1111A", "1111", "a", "Cw4JRyRGXR"
                       You can combine multiple specifiers to specify what you
                       want.
  <alias>              Template's alias. E.g. "cpp"
  ac                   The status of the submission is Accepted.

Examples:
  cf config            Configure the cf-tool.
  cf submit            cf will detect what you want to submit automatically.
  cf submit -f a.cpp
  cf submit https://codeforces.com/contest/100/A
  cf submit -f a.cpp 100A 
  cf submit -f a.cpp 100 a
  cf submit contest 100 a
  cf submit gym 100001 a
  cf list              List all problems' stats of a contest.
  cf list 1119
  cf parse 100         Fetch all problems' samples of contest 100 into
                       "{cf}/{contest}/100/".
  cf parse gym 100001a
                       Fetch samples of problem "a" of gym 100001 into
                       "{cf}/{gym}/100001/a".
  cf parse gym 100001
                       Fetch all problems' samples of gym 100001 into
                       "{cf}/{gym}/100001".
  cf parse             Fetch samples of current problem into current path.
  cf gen               Generate a code from default template.
  cf gen cpp           Generate a code from the template whose alias is "cpp"
                       into current path.
  cf test              Run the commands of a template in current path. Then
                       test all samples. If you want to add a new testcase,
                       create two files "inK.txt" and "ansK.txt" where K is
                       a string with 0~9.
  cf watch             Watch the first 10 submissions of current contest.
  cf watch all         Watch all submissions of current contest.
  cf open 1136a        Use default web browser to open the page of contest
                       1136, problem a.
  cf open gym 100136   Use default web browser to open the page of gym
                       100136.
  cf stand             Use default web browser to open the standing page.
  cf sid 52531875      Use default web browser to open the submission
                       52531875's page.
  cf sid               Open the last submission's page.
  cf race 1136         If the contest 1136 has not started yet, it will
                       countdown. When the countdown ends, it will open all
                       problems' pages and parse samples.
  cf pull 100          Pull all problems' latest codes of contest 100 into
                       "./100/<problem-id>".
  cf pull 100 a        Pull the latest code of problem "a" of contest 100 into
                       "./100/<problem-id>".
  cf pull ac 100 a     Pull the "Accepted" or "Pretests passed" code of problem
                       "a" of contest 100.
  cf pull              Pull the latest codes of current problem into current
                       path.
  cf clone naveen_21tyagi      Clone all codes of naveen_21tyagi.
  cf upgrade           Upgrade the "cf" to the latest version from GitHub.

File:
  cf will save some data in some files:

  "~/.cf/config"        Configuration file, including templates, etc.
  "~/.cf/session"       Session file, including cookies, handle, password, etc.

  "~" is the home directory of current user in your system.

Template:
  You can insert some placeholders into your template code. When generate a code
  from the template, cf will replace all placeholders by following rules:

  $%U%$   Handle (e.g. naveen_21tyagi)
  $%Y%$   Year   (e.g. 2019)
  $%M%$   Month  (e.g. 04)
  $%D%$   Day    (e.g. 09)
  $%h%$   Hour   (e.g. 08)
  $%m%$   Minute (e.g. 05)
  $%s%$   Second (e.g. 00)

Script in template:
  Template will run 3 scripts in sequence when you run "cf test":
    - before_script   (execute once)
    - script          (execute the number of samples times)
    - after_script    (execute once)
  You could set "before_script" or "after_script" to empty string, meaning
  not executing.
  You have to run your program in "script" with standard input/output (no
  need to redirect).

  You can insert some placeholders in your scripts. When execute a script,
  cf will replace all placeholders by following rules:

  $%path%$   Path to source file (Excluding $%full%$, e.g. "/home/naveen_21tyagi/")
  $%full%$   Full name of source file (e.g. "a.cpp")
  $%file%$   Name of source file (Excluding suffix, e.g. "a")
  $%rand%$   Random string with 8 character (including "a-z" "0-9")
```

## Template Example

The placeholders inside the template will be replaced with the corresponding content when you run `cf gen`.

```
$%U%$   Handle (e.g. naveen_21tyagi)
$%Y%$   Year   (e.g. 2019)
$%M%$   Month  (e.g. 04)
$%D%$   Day    (e.g. 09)
$%h%$   Hour   (e.g. 08)
$%m%$   Minute (e.g. 05)
$%s%$   Second (e.g. 00)
```

```cpp
/* Generated by powerful Codeforces Tool
 * Author: $%U%$
 * Time: $%Y%$-$%M%$-$%D%$ $%h%$:$%m%$:$%s%$
**/

#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    
    return 0;
}
```
