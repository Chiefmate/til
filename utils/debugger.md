# Debugger

## LLDB Debugger


gcc에서 -g 옵션을 넣어준다. `lldb filename`을 실행한다.
```sh
$ gcc -g filename
$ lldb ./filename
```


lldb 실행 중 커맨드
```sh
b main      # main 함수에 breakpoint를 설정한다
r           # run
n           # next
print ptr   # 변수 ptr의 값을 출력한다
q           # 종료한다
```

[LLDB Commands Summary](https://aaronbloomfield.github.io/pdr/docs/lldb_summary.html)