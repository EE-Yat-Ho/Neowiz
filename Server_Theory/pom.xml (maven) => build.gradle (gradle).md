pom.xml (maven) => build.gradle (gradle)

Maven에서의 환경설정 파일은 pom.xml
Gradle에서의 환경설정 파일은 build.gradle

pom.xml
~~~
<dependencies>
    <dependency>
        <groupId>그룹</groupId>
        <artifactId>아티팩트</artifactId>
        <version>버전</version>
        <scope>스코프</scope>
    </dependency>
</dependencies>
~~~

build.gradle
~~~
dependencies {
    compile group: '그룹', name: '아티팩트', version: '버전'
}
~~~
or
~~~
dependencies {
    compile('그룹:아티팩트:버전')
}
~~~

왜 안되나했더니.. 의존성 주입 후 설치? 실행?하는 절차가 하나 더 필요함

우측 상단 쯤에 리프레쉬 모양 코끼리가 하나 뜰건데, 그거 누르면됨 와ㅏㅏㅏ

