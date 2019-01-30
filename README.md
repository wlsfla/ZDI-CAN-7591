# ZDI-CAN-7591
Windows Contact File HTML Injection Mailto: Link RCE 0day / ZDI-CAN-7591


1. ``윈도우 탐색기 - 우클릭 - 새로 만들기 - 연락처(.contact)`` 파일 생성
2. 하단의 ``전자 메일`` 항목에 ``<a href="calc.exe">test@test.com</a>`` 추가
3. ``연락처(.contact)`` 파일을 실행하고 ``요약 - 전자 메일``의 이메일 주소를 선택하면 경고창 없이 명령어가 실행된다.

====================================

번역)
이것은 내가 ZDI에 보고한 서로 다른 세가지 취약점 중 한가지입니다.
이것은 Microsoft가 고치지 않기로 한 것입니다. .VCF파일과 두개의 .Contact 윈도우즈 파일 이슈입니다.

이 취약점은 MS 윈도우즈의 취약한 설치 도중 원격 공격자가 임의의 코드를 실행하는 것을 허용한다.

유저 상호작용이 요구되어진다. 상호작용 : 타겟이 malicious 페이지를 방문하거나 malicious 파일을 Open해야 한다는 점

이 취약점의 결점은 .contact 파일을 처리하는 과정때문이다. 이메일 주소 필드에 예상되는 이메일 주소값을 할당하지만 .contact 파일은 html 인젝션에 취약하다. 그래서 공격자가 실행할 수 있는 파일을 HREF html tag를 사용하여 참조하면 경고창 없이 실행할 것이다. 예상할 수 있는 이메일 등록 행위 대신에


예시:
<a href="calc.exe">pwn@microsoft.com</a>


출처:
https://cxsecurity.com/issue/WLB-2019010225
https://vimeo.com/312824315

원문
This was the last of three different vulnerabilities I reported to ZDI that Microsoft choose not to fix, a .VCF file and two .Contact Windows file issues.

This vulnerability allows remote attackers to execute arbitrary code on vulnerable installations of Microsoft Windows.
User interaction is required to exploit this vulnerability in that the target must visit a malicious page or open a malicious file.

The flaw is due to the processing of ".contact" files, the E-mail address field takes an expected E-mail address value, however the .CONTACT file is
vulnerable to HTML injection so if an attacker references an executable file using an HREF tag it will run that instead without warning instead of
performing the expected email behavior. This is dangerous and would be unexpected to an end user.
