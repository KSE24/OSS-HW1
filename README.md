# OSS-HW1

## 1. getopt



## 2. getopts




## 3. sed
```
sed [OPTION] {script-only-if-no-other-script} [input-file]
```
> **텍스트를 필터링, 변형하기 위한 스트림 에디터**
- _수정, 치환, 삭제, 추가 등 편집기 기능_
- _파일을 인자로 받아 명령어를 통해 작업_
- _원본이 손상, 변형 되지 않음_

<br/>

> **OPTION**
* _-e : sed 명령어를 사용하였을 때 출력되는 값을 보여줌_
* _-i : 변경되는 값을 출력 없이 바로 저장_
* _-n : 특정 값의 행만 출력_
* _-f : 스크립트를 파일로부터 읽어들여서 명령어로 지정_

<br/>

> **sed 명령어**
* p : 출력
   * 
* d : 삭제
   * 
* s : 치환
   * 






## 4. awk
```
awk [OPTION] [awk program] [ARGUMENT]
```
> **파일에서 일치하는 내용을 찾아서 지정한 패턴을 수행 후 출력하는 명령어**
- _텍스트 파일의 전체 내용 출력_
- _파일의 특정 필드만 출력_
- _특정 필드에 문자열을 추가해서 출력_
- _패턴이 포함된 레코드 출력_
- _특정 필드에 연산 수행 결과 출력_
- _필드 값 비교에 따라 레코드 출력_

<br/>

> **OPTION**
* _-F : 필드 구분 문자 지정_
* _-f : awk program 파일 경로 지정_
* _-v : awk program에서 사용될 특정 variable값 지정_

<br/>

> **awk program**
* _pattern {action} 형태_
    * _patern을 생략하면 : "모든 레코드" 적용_
    * _action을 생략하면 : "print" 적용_

<br/>

> **awk program language**
* _표현식_
```
    (E)    $n     ++E    --E    E++    E--    E^E    !E     +E      V-=E
    -E     E*E    E/E    E%E    E+E    E-E    E E    E<E    E<=E    V=E
    E!=E   E==E   E>E    E>=E   E~E    E!-E   E in array     (n) in array 
    E&&E   E||E   E1?E2:E3      V^=E   V%=E   V*=E   V/=E   V+=E
```
* _키워드_
```
    BEGIN    delete      END       function     in          printf     break      do      print
    exit     getline     next      return       continue    else       for        if      while
```
* _미리 정의 된 변수_
```
    ARGC        : ARGV 배열 요소의 갯수
    ARGV        : command line argument에 대한 배열
    CONVFMT     : 문자열을 숫자로 변경할 때 사용할 형식 (ex, "%.6g")
    ENVIRON     : 환경변수에 대한 배열
    FILENAME    : 경로를 포함한 입력 파일 이름
    FNR         : 현재 파일에서 현재 레코드의 순서 값
    FS          : 필드 구분 문자 (기본 값 = space)
    NF          : 현재 레코드에 있는 필드의 갯수
    NR          : 입력 시작 점에서 현재 레코드의 순서 값
    OFMT        : 문자열을 출력할 때 사용할 형식
    OFS         : 결과 출력 시 필드 구분 문자 (기본 값 = space)
    ORS         : 결과 출력 시 레코드 구분 문자 (기본 값 = newline)
    RLENGTH     : match 함수에 의해 매칭된 문자열의 길이
    RS          : 레코드 구분 문자 (기본 값 = newline)
    RSTART      : match 함수에 의해 매칭된 문자열의 시작 위치
```
* _사용 가능한 함수_
```
Arithmetic Functions :
    atan2(y,x),     cos(x),     sin(x),     exp(x),     log(x),     sqrt(x),
    int(x),         rand(),     srand([expr])

String Functions :
    gsub(ere, repl[, in]),      index(s, t),            length[([s])],
    match(s, ere),              split(s, a[, fs ]),     sprintf(fmt, expr, expr, ...),
    sub(ere, repl[, in ]),      substr(s, m[, n ]),     tolower(s),
    toupper(s)

Input/Output and General Functions :
    close(expression),          getline                 getline var
    system(expression)
```    

<br/>

> **awk 사용 예시**


|예시|명령어 옵션|
|-|-|
|파일의 전체 내용 출력	|awk '{ print }' [FILE]|
|필드 값 출력	|awk '{ print $1 }' [FILE]|
|필드 값에 임의 문자열을 같이 출력	|awk '{print "STR"$1, "STR"$2}' [FILE]|
|지정된 문자열을 포함하는 레코드만 출력	|awk '/STR/' [FILE]|
|특정 필드 값 비교를 통해 선택된 레코드만 출력	|awk '$1 == 10 { print $2 }' [FILE]|
|특정 필드들의 합 구하기	|awk '{sum += $3} END { print sum }' [FILE]|
|여러 필드들의 합 구하기|awk '{ for (i=2; i<=NF; i++) total += $i }; END { print "TOTAL : "total }' [FILE]|
|레코드 단위로 필드 합 및 평균 값 구하기|awk '{ sum = 0 } {sum += ($3+$4+$5) } { print $0, sum, sum/3 }' [FILE]|
|필드에 연산을 수행한 결과 출력하기|awk '{print $1, $2, $3+2, $4, $5}' [FILE]|
|레코드 또는 필드의 문자열 길이 검사	|awk ' length($0) > 20' [FILE]|
|파일에 저장된 awk program 실행	|awk -f [AWK FILE] [FILE]|
|필드 구분 문자 변경하기	|awk -F ':' '{ print $1 }' [FILE]|
|awk 실행 결과 레코드 정렬하기	|awk '{ print $0 }' [FILE]|
|특정 레코드만 출력하기	|awk 'NR == 2 { print $0; exit }' [FILE]|
|출력 필드 너비 지정하기	|awk '{ printf "%-3s %-8s %-4s %-4s %-4s\n", $1, $2, $3, $4, $5}' [FILE]|
|필드 중 최대 값 출력	|awk '{max = 0; for (i=3; i<NF; i++) max = ($i > max) ? $i : max ; print max}' [FILE]|
