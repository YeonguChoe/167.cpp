# C# 언어 설정

- 컴파일 환경: C#10 on .NET 6.0 runtime

### Writing data to a file
```C#
TextWriter textWriter = new StreamWriter(@System.Environment.GetEnvironmentVariable("OUTPUT_PATH"), true);
```

- System.Environment.GetEnvironmentVariable("<환경 변수 이름>")
  - 환경변수의 값을 반환한다.
  - ```C#
    string desktopPath = System.Environment.GetEnvironmentVariable("Desktop");
    ```
  -  documentaion: https://learn.microsoft.com/en-us/dotnet/api/system.environment.getenvironmentvariable?view=net-8.0

- Verbatism text `@`
  - `@`을 붙이면, escape sequence (`\n`, `\t`, `\\)들이 키워드가 아니라 문자 그대로 해석된다.
  - ```C#
    string path = @"C:\Users\yeong\OneDrive\Desktop";
    ```
  - documentation: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/verbatim


- TextWriter 클래스
  - abstract 클래스라서 객체화를 할 수 없다.
  - 하위 클래스인 StreamWriter을 이용해서 객체화 할 수 있다.
  - ```C#
    // 이렇게 하면 TextWriter에 있는 기능만 사용할 수 있다.
    TextWriter textWriter = new StreamWriter(path, true);
    ```
  - 두번째 매개변수는 기존 파일에 내용을 추가 할지 여부이다.
  - documentation: https://learn.microsoft.com/en-us/dotnet/api/system.io.textwriter

- StreamWriter 클래스
  - 텍스트 Stream을 만든다.
  - 파일에 텍스트 데이터를 입력하는데 사용한다.
  - ```C#
    StreamWriter textWriter = new StreamWriter(path, true);
    ```
  - documentation: https://learn.microsoft.com/en-us/dotnet/api/system.io.streamwriter

```C#
textWriter.Write("Sentence");
```
 
- Write(<내용>)
  - 문자열을 텍스트 Stream에 추가한다.
  -  documentation: https://learn.microsoft.com/en-us/dotnet/api/system.io.textwriter.write?view=net-8.0#system-io-textwriter-write(system-string)

```C#
textWriter.WriteLine("Sentence");
```

- WriteLine(<내용>)
  - 문자열과 줄바꿈 문자 `\n`를 텍스트 Stream에 추가한다.
  - documentation: https://learn.microsoft.com/en-us/dotnet/api/system.io.streamwriter.writeline?view=net-8.0#system-io-streamwriter-writeline(system-string)

```C#
textWriter.Flush();
```

- Flush()
  - 버퍼에 있는 데이터를 Stream으로 옮긴다.
  - documentation: https://learn.microsoft.com/en-us/dotnet/api/system.io.streamwriter.flush?view=net-8.0#system-io-streamwriter-flush

```C#
textWriter.Close();
```

- Close()
  - Writer 객체를 없애고 디스크와의 연결을 해제한다.
  - documentation: https://learn.microsoft.com/en-us/dotnet/api/system.io.textwriter.close?view=net-8.0#system-io-textwriter-close
