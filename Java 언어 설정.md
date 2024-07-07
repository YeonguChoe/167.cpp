# Java 언어 설정

- 컴파일 환경: OpenJDK 17.0.1

### File Writer

```java
BufferedWriter bw = new BufferedWriter(new FileWriter("<파일이름>"));
```

- FileWriter
    - 파일에 데이터를 기록하는 기능을 하는 클래스이다.
    - ```java 
        // FileWriter fw = new FileWriter("<파일 이름>"); // 덮어쓰기 (overwrite): 파일의 모든 데이터가 새로 쓰여진다.
        FileWriter fw = new FileWriter("파일 이름", true); // 추가하기 (append): 파일의 기존 데이터의 끝에 새로운 내용을 추가한다.
        fw.write("<내용>"); // text를 파일에 쓴다.
        fw.close(); // close를 해야지만 디스크에 저장이 된다.```
    - default 버퍼 크기인 8K(8192) Byte를 사용한다.
    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/io/FileWriter.html

- BufferedWriter
    - 파일에 데이터를 직접 쓰지 않고, 버퍼에 일시적으로 저장했다가 한번에 파일에 기록하는 기능을 FileWriter에 제공하는 클래스이다.
    - FileWriter만 사용해서 파일에 데이터를 저장할 수 있지만, BufferedWriter를 이용해서 성능 개선을 한다.
    - ```java         
        BufferedWriter bw = new BufferedWriter(new FileWriter("<파일 이름>"), <버퍼 크기(Byte)>);
        bw.write("<내용>");
        bw.close(); // close를 안하면 저장이 안된다.```
    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/io/BufferedWriter.html

