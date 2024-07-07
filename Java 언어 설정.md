# Java 언어 설정

- 컴파일 환경: OpenJDK 17.0.1

### Writing data to a file

```java
// OUTPUT_PATH 환경 변수에 지정된 경로에 새 파일을 만들고, 데이터를 파일에 출력할수 있도록 버퍼를 만든다.
BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));
```

- System.getenv
    - 운영체제에 저장된 환경변수를 String으로 반환한다.
    - ```java
      System.getenv("<환경변수 이름>")
      ```
    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/lang/System.html#getenv()

- FileWriter
    - 파일에 데이터를 기록하는 기능을 하는 클래스이다.
    - ```java 
        // FileWriter fw = new FileWriter("<파일 이름>"); // 덮어쓰기 (overwrite): 파일의 모든 데이터가 새로 쓰여진다.
        FileWriter fw = new FileWriter("파일 이름", true); // 추가하기 (append): 파일의 기존 데이터의 끝에 새로운 내용을 추가한다.
        fw.write("<내용>"); // text를 파일에 쓴다.
        fw.close(); // close를 해야지만 디스크에 저장이 된다.
      ```
    - default 버퍼 크기인 8K(8192) Byte를 사용한다.
    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/io/FileWriter.html

- BufferedWriter
    - 파일에 데이터를 직접 쓰지 않고, 버퍼에 일시적으로 저장했다가 한번에 파일에 기록하는 기능을 FileWriter에 제공하는 클래스이다.
    - FileWriter만 사용해서 파일에 데이터를 저장할 수 있지만, BufferedWriter를 이용해서 성능 개선을 한다.
    - ```java         
        BufferedWriter bw = new BufferedWriter(new FileWriter("<파일 이름>"), <버퍼 크기(Byte)>);
        bw.write("<내용>");
        bw.close(); // close를 안하면 저장이 안된다.
      ```

    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/io/BufferedWriter.html

### Reading data from a file

```java
// 사용자가 키보드를 통해 입력하는 문자열을 읽기 위한 버퍼를 만든다. 
BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
```

- InputStreamReader
    - Input stream을 char 기반 스트림으로 변환해준다.
    - ```java
        InputStreamReader isr = new InputStreamReader(System.in); // 키보드의 Input Stream을 char Stream으로 변환해주는 객체를 만든다.
        int letter1 = isr.read(); // 콘솔에서 1글자를 읽어서 유니코드의 값으로 지정한다.
        int letter2 = isr.read(); // 다음 글자를 읽어서 유니코드의 값으로 지정한다.
        int letter3 = isr.read(); // 다음 글자를 읽어서 유니코드의 값으로 지정한다.
      ```
    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/io/InputStreamReader.html

- BufferedReader
    - 데이터를 버퍼에 임시 기록해서 성능을 높여주는 기능을 하는 클래스이다.
    - BufferedReader를 사용하면 사용자의 입력을 한 줄씩 받을 수 있다.
    - ```java 
        InputStreamReader isr = new InputStreamReader(System.in); // 키보드의 Input Stream을 char Stream으로 변환해주는 객체를 만든다.
        BufferedReader br = new BufferedReader(isr, 100); // 100 바이트의 버퍼를 사용하도록 래핑한다.
        String line1 = br.readLine(); // 한줄을 읽는다.
        String line2 = br.readLine(); // 한줄을 더 읽는다.
        String line3 = br.readLine(); // 한줄을 더 읽는다.
      ```
    - documentation: https://docs.oracle.com/en/java/javase/20/docs/api/java.base/java/io/BufferedReader.html

```java
// gEdges번 만큼 반복하면서 파일에서 한 줄씩 읽어 들이고, 각 줄을 공백을 기준으로 gFrom, gTo, gWeight 리스트에 추가한다.
IntStream.range(0, gEdges).forEach(i -> {
    try {
        String[] gFromToWeight = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");
        gFrom.add(Integer.parseInt(gFromToWeight[0]));
        gTo.add(Integer.parseInt(gFromToWeight[1]));
        gWeight.add(Integer.parseInt(gFromToWeight[2]));
    } catch (IOException ex) {
        throw new RuntimeException(ex);
    }
});
```

- IntStream.range(<시작값>, <끝값>)
    - 1개의 정수 Stream을 생성하고 <시작값>부터 <끝값> - 1을 입력한다.
    - ```java
      IntStream.range(1, 30) // 1부터 29까지의 정수를 포함하는 IntStream을 생성
         .forEach(i -> { // 각 정수를 순회하며
             System.out.println(i); // 정수 i를 출력한다.
         });
      ```