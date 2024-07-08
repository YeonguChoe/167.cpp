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

- Verbatism text @
  - `@`을 붙이면, `\\` 또는 `\t` 같은 문자들이 키워드가 아니라 문자 그대로 해석된다.
  - ```C#
    string path = @"C:\Users\yeong\OneDrive\Desktop";
    ```
  - documentation: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/verbatim

- StreamWriter()
