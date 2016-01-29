# Cpulimit

Cpulimit is a program which limits the cpu usage percentage of specificed processes. It can be used to limit the cpu usage of processes that use a large percentage of the cpu, in order to reduce the processing load on the cpu.

## Installation

Install the [cpulimit](https://www.archlinux.org/packages/?name=cpulimit) package.

## Usage

Cpulimit limits the cpu usage of a process using a scale of 0 to 100 times the number of cpu cores that the computer has. For instances with 8 cpu cores, the precentage range will be 0 to 800.

The process that will be limited can be specified by its pid.

```
$ cpulimit -l 50 -p 5081

```

## See also

*   [Cpulimit GitHub repository](https://github.com/opsengine/cpulimit)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Cpulimit&oldid=416565](https://wiki.archlinux.org/index.php?title=Cpulimit&oldid=416565)"