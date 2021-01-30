# DNS & DHCP

</br>

7번째 계층인 응용 계층을 살펴보면 DNS, DHCP라는 것이 있다.

### DNS                           DHCP

Domain Name Server                  Dynamic Host Configuration Protocol

이 둘 모두 IP주소를 어떠한 이름과 연결해주는 것과 관련이 있다.

브라우저창에 머리 아프게 숫자를 입력하지 않고도 [www.google.com](http://www.google.com) 이나 [www.naver.com](http://www.naver.com) 을 입력하여 구글과 네이버의 서버에서 제공하는 서비스에 접근할 수 있게 해주는 것이다.

---

## DNS
**Domain Name Server**

DNS는 특정 주소명을 IP주소로 전환하는 것을 담당한.**

[www.google.com이라는](http://www.google.com%EC%9D%B4%EB%9D%BC%EB%8A%94) 걸 입력받으면 .com 서버에 해당 주소가 어떤 IP주소와 연결되어 있는지를 찾아 그 주소의 데이터를 우리가 접근할 수 있도록 연결을 도와준다.

</br>

DNS가 구체적으로 어떤 절차를 거쳐 이름과 IP주소를 연결시켜주는지는 아래링크 참고 (이 과정을 Domain Name Resolution이라고 한다)

[What is Domain Name System and what is the purpose of the DNS?](https://www.cloudns.net/blog/what-is-dns/)

---

## DHCP

**Dynamic Host Configuration Protocol**

DHCP는 정확히 무엇일까?

**DHCP는 애초에 어떤 IP주소를 특정 웹사이트의 이름에 할당해줄지를 결정하는 프로토콜이다.**

웹사이트를 만들 때 IP주소를 고정할 것 같지만, 실제 IP주소의 할당은 생각보다 훨씬 동적이다.

하나하나 주소를 다 고정시키기엔 손도 많이 가고, 무엇보다 위에서부터 끊임없이 이야기해오던 주소 고갈의 문제가 있다.

그래서 고안한 방법이, 현재 사용 중이지 않거나 대여 기간이 끝난 IP주소는 또 다른 곳에 할당을 해주는 것이다.

이렇게 DNS가 전달받은 이름을 IP주소와 매치시키기 전에 애초에 할당을 해주는 과정과 관계된 것이 DHCP이다.

DHCP 서버와 연동만 되어 있다면 이런 일련의 과정이 모두 자동화될 수 있는 것이 장점이라고 한다.


---

</br>

**[참고 및 출처]**

[링크1](https://stitchcoding.tistory.com/4)
