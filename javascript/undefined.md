# 📔 들어가며

이 GitBook 저의 JavaScript 공부를 위해 만들게 되었습니다. 참고와 공부를 위한 서적은 `<자바스크립트 DeepDive>`를 보며 정리를 하고, 중요한 내용들은 사이사이에 `Key Point`를 넣었습니다. 그리고 해당 카테고리별 마지막에는 `요약`을 구성하며 복습하거나 빠르게 그 파트의 내용을 알 수 있도록 하였습니다.

##

## 목차

1. [변수](04./)
   1. [변수의 정의](04./4.1\_.md)
   2. [식별자](04./4.2\_.md#undefined)
   3. [변수 선언](04./4.3\_.md#undefined)
   4. [변수 호이스팅](04./4.4\_.md)
   5. [값의 할당 재할당](04./4.5\_.md)
   6. [식별자 네이밍 규칙](04./4.6\_.md)
2. [표현식과 문](05./)
   1. [값과 리터럴](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/05.%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC%20%EB%AC%B8/5.1\_%EA%B0%92%EA%B3%BC%20%EB%A6%AC%ED%84%B0%EB%9F%B4.md)
   2. [표현식과 문](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/05.%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC%20%EB%AC%B8/5.3\_%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC%20%EB%AC%B8.md)
   3. [세미콜론과 자동삽입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/05.%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC%20%EB%AC%B8/5.5\_%EC%84%B8%EB%AF%B8%EC%BD%9C%EB%A1%A0%EA%B3%BC%20%EC%9E%90%EB%8F%99%EC%82%BD%EC%9E%85%EA%B8%B0%EB%8A%A5.md)
3. [데이터 타입](https://github.com/ohtaekwon/Frontend-101/tree/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85) -[숫자 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   1. [문자열 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   2. [템플릿 리터럴](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   3. [불리언 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   4. [undefined 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   5. [null 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   6. [심벌 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   7. [객체 타입](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
   8. [타입의 필요성](https://github.com/ohtaekwon/Frontend-101/blob/main/JavaScript/DeepDive/06.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85/6.1\_%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%83%80%EC%9E%85\(%EC%88%AB%EC%9E%90%2C%20%EB%AC%B8%EC%9E%90%EC%97%B4%2C%20%EB%B6%88%EB%A6%AC%EC%96%B8\).md#61-%EC%88%AB%EC%9E%90-%ED%83%80%EC%9E%85)
4.  [연산자](../JavaScript/DeepDive/07.%EC%97%B0%EC%82%B0%EC%9E%90)

    1. [산술 연산자](07./07.1\_.md#71-산술-연산자)
    2. [할당 연산자](07./07.1\_.md#72-할당-연산자)
    3. [비교 연산자](07./07.1\_.md#73-비교-연산자)
    4. [삼항조건연산자](07./07.2\_-typeof.md#74-삼항-조건-연산자)
    5. [논리 연산자](07./07.2\_-typeof.md#75-논리-연산자)
    6. [쉼표 연산자](07./07.2\_-typeof.md#76-쉼표-연산자)
    7. 그룹 연산자
    8. typeof 연산자



