# Code Modification

Yang diubah dalam XV6 :
## Makefile  

Line 3-4 : 
```c
CS333_PROJECT ?= 1
PRINT_SYSCALLS ?= 1
```
Line 16 : 
```c
CS333_UPROGS += _date
```

## proc.c

Line 152 : 
```c
p->start_ticks = ticks;
```

Line 567-573 : 
```c
   #ifdef CS333_P1
  int elapsed_millisec = ticks - p->start_ticks;
  int elapsed_sec = elapsed_millisec / 1000;
  int modulo_elapsed =  elapsed_millisec % 1000;
  cprintf("%d\t%s\t\t%d.%d\t%s\t%d\t" , p->pid, p->name, elapsed_sec, modulo_elapsed, state_string, p->sz);
  return;
  #endif // CS333_P1S
```

## proc.h

Line 52 : 
```c
uint start_ticks;
```

## syscall.c

Line 109-112 : 
```c
#ifdef CS333_P1
extern int sys_date(void);
#endif
```
Line 139-141 : 
```c
#ifdef CS333_P1
// internally, the function prototype must be ’int’ not ’uint’ for sys_date()
[SYS_date]    sys_date,
#endif
```
Line 182-185 : 
```c
    #ifdef PRINT_SYSCALLS
    cprintf("%s -> %d\n",
            syscallnames[num], curproc->tf->eax);
    #endif
```

## syscall.h

Line 24 : 
```c
#define SYS_date    SYS_halt+1
```

## sysproc.c

Line 101-111 : 
```c
#ifdef CS333_P1
int
sys_date(void)
{
  struct rtcdate *d;
  if(argptr(0, (void*)&d, sizeof(struct rtcdate)) < 0)
    return -1;
  cmostime(d);
  return 0;
}
#endif
```

## user.h

Line 28-30 : 
```c
#ifdef CS333_P1
int date(struct rtcdate*);
#endif
```

## usys.S

Line 33 : 
```c
SYSCALL(date)
```
